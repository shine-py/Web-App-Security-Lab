# Web-App-Security-Lab

Лабораторный стенд для изучения веб-атак и механизмов защиты веб-приложений.

### Архитектура
- Kali - хост атакующего
- Ubuntu - защищаемый сервер
- DVWA (Damn Vulnerable Web Application)
- SafeLine WAF

## Шаги проекта

- Настроены виртуальные машины Ubuntu (защищаемый сервер) и Kali (атакующий) в сетевом режиме VMware - NAT, изолируя виртуальные машины от локальной сети и интернета.
- Установил SafeLine WAF на Ubuntu и разместил на порту 9443.

<img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/9b0769dc-d0b9-40b9-aca0-bd88aac9bf1d" />

<img width="2509" height="1170" alt="image" src="https://github.com/user-attachments/assets/8c1d7274-de56-425a-807e-263766799938" />

- Установил веб-сервер Apache и развернул приложение DVWA на Ubuntu на порту 8080.

<img width="800" height="500" alt="image" src="https://github.com/user-attachments/assets/f4a47320-59d1-4f6f-b935-ab6e095dea93" />
