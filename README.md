# Домашнее задание к занятию "`Защита сети`" - `Макаров Денис`

<details>
### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)
</details>


### Задание 1
Проведите разведку системы и определите, какие сетевые службы запущены на защищаемой системе:

**sudo nmap -sA < ip-адрес >**

**sudo nmap -sT < ip-адрес >**

**sudo nmap -sS < ip-адрес >**

**sudo nmap -sV < ip-адрес >**

По желанию можете поэкспериментировать с опциями: https://nmap.org/man/ru/man-briefoptions.html.


*В качестве ответа пришлите события, которые попали в логи Suricata и Fail2Ban, прокомментируйте результат.*

### Ответ:
Усатновленные программы представлены на скриншотах ниже:

Suricata:

![Suricata](https://github.com/Makarov-Denis/12_03-Network_protection/assets/148921246/b8ac7a46-396a-4bfa-8eaf-e83bfe584345)

Fail2ban:

![Fail2ban](https://github.com/Makarov-Denis/12_03-Network_protection/assets/148921246/e24f4a85-a68e-4c82-8b20-8b2f5d53491f)

sudo nmap -sA 192.168.1.2

![nmap -sA](https://github.com/Makarov-Denis/12_03-Network_protection/assets/148921246/3c90eea7-b9c2-4ec2-8f0a-8a4f45e1a655)

![лог -sA](https://github.com/Makarov-Denis/12_03-Network_protection/assets/148921246/67af0de6-3fee-4d42-b144-d44ff13e4f30)

sudo nmap -sT 192.168.1.2

![nmap -sT](https://github.com/Makarov-Denis/12_03-Network_protection/assets/148921246/327611e3-9235-4bee-ab42-0c1e3580e582)

![лог -sT](https://github.com/Makarov-Denis/12_03-Network_protection/assets/148921246/50e866c6-7d5f-45e9-a248-e553a46263b4)

sudo nmap -sS 192.168.1.2

![nmap -sS](https://github.com/Makarov-Denis/12_03-Network_protection/assets/148921246/b77c5688-e8b3-4be4-a08b-48a71a82f3ea)

![лог -sS](https://github.com/Makarov-Denis/12_03-Network_protection/assets/148921246/42deec5b-97cd-4eb4-ad5c-bb134273c183)

sudo nmap -sV 192.168.1.2

![nmap -sV](https://github.com/Makarov-Denis/12_03-Network_protection/assets/148921246/14b6d769-0476-4ebb-b6a3-8aa9439d2e6b)


![лог -sV](https://github.com/Makarov-Denis/12_03-Network_protection/assets/148921246/513a4e17-cf39-4625-8921-da68ddfed16b)

fail2ban на сканирования не отреагировал

---

### Задание 2

Проведите атаку на подбор пароля для службы SSH:

**hydra -L users.txt -P pass.txt < ip-адрес > ssh**

1. Настройка **hydra**: 
 
 - создайте два файла: **users.txt** и **pass.txt**;
 - в каждой строчке первого файла должны быть имена пользователей, второго — пароли. В нашем случае это могут быть случайные строки, но ради эксперимента можете добавить имя и пароль существующего пользователя.

Дополнительная информация по **hydra**: https://kali.tools/?p=1847.

2. Включение защиты SSH для Fail2Ban:

-  открыть файл /etc/fail2ban/jail.conf,
-  найти секцию **ssh**,
-  установить **enabled**  в **true**.

Дополнительная информация по **Fail2Ban**:https://putty.org.ru/articles/fail2ban-ssh.html.



*В качестве ответа пришлите события, которые попали в логи Suricata и Fail2Ban, прокомментируйте результат.*

### Ответ:

С выключенным сервисом *Fail2Ban* сканирование прошло успешно.</br>

![hydra](https://github.com/Makarov-Denis/12_03-Network_protection/assets/148921246/0df25bf2-2645-431f-9fda-a7902da2baca)

Sucirata среагировала:
![лог hydra suricata](https://github.com/Makarov-Denis/12_03-Network_protection/assets/148921246/f21a4d02-8431-4db1-9313-52c14e79255f)

После включения Fail2ban

![Fail2ban2](https://github.com/Makarov-Denis/12_03-Network_protection/assets/148921246/9303057a-c8b5-4670-9184-9c8811e795e7)

Sucirata 

![лог hydra suricata](https://github.com/Makarov-Denis/12_03-Network_protection/assets/148921246/02260493-cb69-4c9c-a3e7-0d08c4c0307c)

Fail2ban

![лог hydra fail2ban](https://github.com/Makarov-Denis/12_03-Network_protection/assets/148921246/12084e92-42da-4fe2-b5ed-d73857c6fd3c)


