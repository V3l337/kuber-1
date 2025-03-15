# Домашнее задание к занятию «Kubernetes. Причины появления. Команда kubectl»

## Задание 1. Установка MicroK8S

1. **Установить MicroK8S на локальную машину или на удалённую виртуальную машину.**
   - Установил с помощью `snap`:
     ```bash
     sudo snap install microk8s --classic
     ```

2. **Установить dashboard.**
   - Для установки dashboard использовал команду:
     ```bash
     microk8s enable dashboard
     ```

3. **Сгенерировать сертификат для подключения к внешнему IP-адресу.**
   - Проверил текущую конфигурацию:
     ```bash
     microk8s config
     ```
   - Изменил IP адрес сервера и обновил файл конфигурации:
     ```bash
     microk8s kubectl config view --raw > ~/.kube/config
     ```
   - Обновил сертификаты:
     ```bash
     sudo microk8s refresh-certs --cert front-proxy-client.crt
     ```

## Задание 2. Установка и настройка локального kubectl

1. **Установить на локальную машину kubectl.**
   - Установил через `snap`:
     ```bash
     sudo snap install kubectl --classic
     ```

2. **Настроить локальное подключение к кластеру.**
   - Конфигурация уже была настроена ранее в рамках первого задания.
   - В файле `/var/snap/microk8s/current/certs/csr.conf.template` проверил IP-адреса и добавил внешний IP.

3. **Подключиться к дашборду с помощью port-forward.**
   - Первая попытка подключения с использованием команды:
     ```bash
     microk8s kubectl port-forward -n kube-system service/kubernetes-dashboard 10443:443
     ```
     Неудачна, так как она проксирует трафик только для локального хоста.

   - Вторая попытка с добавлением параметра `--address 0.0.0.0` для проксирования на все интерфейсы:
     ```bash
     microk8s kubectl port-forward -n kube-system service/kubernetes-dashboard 10443:443 --address 0.0.0.0
     ```

## Скриншоты

1. Скриншот вывода команды `kubectl get nodes`.
![вывода команд kubectl get nodes ](https://github.com/user-attachments/assets/c7772852-e2c3-4928-9bf3-966152cf1a6d)

2. Скриншот с дашбордом.
![скриншот дашборда](https://github.com/user-attachments/assets/a86d4d85-fd45-43c5-b785-04d0a28f3731)


