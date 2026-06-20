# Стенд DVWA для анализа веб-атак с использованием WAF

Лабораторный стенд для изучения веб-атак и механизмов защиты веб-приложений.

### Архитектура
- Kali - хост атакующего
- Ubuntu - защищаемый сервер
- DVWA (Damn Vulnerable Web Application)
- SafeLine WAF

### Полученные навыки
- Администрирование WAF
- Анализ событий ИБ
- Развертывание изолированных сред тестирования (VMware)

## Шаги проекта

- Настроены виртуальные машины Ubuntu (защищаемый сервер) и Kali (атакующий) в сетевом режиме VMware - NAT, изолируя виртуальные машины от локальной сети и интернета.
- Установил SafeLine WAF на Ubuntu и разместил на порту 9443.

  <img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/9b0769dc-d0b9-40b9-aca0-bd88aac9bf1d" />
  
  <img width="2509" height="1170" alt="image" src="https://github.com/user-attachments/assets/8c1d7274-de56-425a-807e-263766799938" />

- Установил веб-сервер Apache и развернул приложение DVWA на Ubuntu на порту 8080.

  <img width="800" height="500" alt="image" src="https://github.com/user-attachments/assets/f4a47320-59d1-4f6f-b935-ab6e095dea93" />

- Сгенерировал самоподписанный SSL сертификат через OpenSSL и добавил его в WAF.
- Сконфигурировал Reverse Proxy: HTTPS-трафик принимается WAF на порту 443 и перенаправляется на порт DVWA (8080).

  <img width="593" height="647" alt="image" src="https://github.com/user-attachments/assets/91719022-a782-4ba5-892c-b508ccd2cd8f" />
  
  <img width="539" height="166" alt="image" src="https://github.com/user-attachments/assets/b28fcf66-c2f7-4bdf-a77e-1d38c8699e05" />

- Теперь при обращении из Kali Linux по адресу WAF успешно перенаправляет его на HTTPS и транслирует интерфейс авторизации DVWA.
  
  <img width="1051" height="630" alt="image" src="https://github.com/user-attachments/assets/2a6ce9dc-c27c-4e74-86cf-5eb1bd1d248c" />

- Провел симуляцию веб-атаки из Kali Linux, отправив классический вектор SQL-инъекции (`' OR 1=1 --`).
  
  <img width="901" height="390" alt="image" src="https://github.com/user-attachments/assets/9d889f5f-3620-4eb1-be34-8acde344f49e" />

- Успешно подтвердил работу SafeLine WAF: вредоносный запрос был заблокирован, атакующему возвращена страница блокировки, а DVWA остался в безопасности.
  
  <img width="2553" height="1220" alt="image" src="https://github.com/user-attachments/assets/f44594b1-e0c4-4831-99b4-ae90dae2357a" />

- Проанализировал зарегистрированный инцидент в консоли мониторинга SafeLine WAF (раздел Attacks/Events). WAF корректно определил IP-адрес источника угрозы (Kali Linux: 192.168.142.131), URL цели атаки и зафиксировал единичную попытку эксплуатации уязвимости.

  <img width="1274" height="489" alt="image" src="https://github.com/user-attachments/assets/067960be-23ad-4b9f-bc37-1c0c26088d91" />

- Проанализировал логи WAF во вкладке LOGS: система успешно классифицировала угрозу как SQL-инъекцию (Attack Type: SQL Inj) и зафиксировала тип действия (Action: Blocked).
  
  <img width="1773" height="397" alt="image" src="https://github.com/user-attachments/assets/13db4615-ca00-4217-b007-8c6470e5f121" />


- Во вкладке Detail можно просмотреть событие детальнее и увидеть содержание HTTP-запроса.
  
  <img width="600" height="450" alt="image" src="https://github.com/user-attachments/assets/ab42b3de-dd83-4438-9ed7-47faa7096177" />


