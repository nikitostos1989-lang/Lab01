# Анализ вредоносного ПО: Lab01-01.exe и Lab01-01.dll

##  Общая информация
- **Дата анализа:** [24.11.2025]
- **Аналитик:** [Смирнов Никита]
- **Образцы:** Lab01-01.exe, Lab01-01.dll

##  Краткое описание
Данный отчет содержит результаты статического анализа двух связанных вредоносных файлов...

##  Результаты анализа

#### Вопрос 1: 1.Загрузите файлы на сайт www.VirusTotal.com и просмотрите отчет. Соответствует ли каждый из 
#### них имеющимся антивирусным сигнатурам?**

**Файл:** Lab01-01.exe
- **Результат:** 56/70 антивирусов детектируют как malicious
- **Платформа:** VirusTotal

**Файл:** Lab01-01.dll  
- **Результат:** 39/70 антивирусов детектируют как malicious
- **Платформа:** VirusTotal
![Screenshot_2](https://github.com/user-attachments/assets/07f50695-ed53-43b5-b5e7-45e3fe1747cc)
![Screenshot_4](https://github.com/user-attachments/assets/e3b8e1db-11e0-4666-a2ac-0c79047e2a47)


#### Вопрос 2: Когда эти файлы были скомпилированы?
**Lab01-01.exe:** 2010-12-19 16:16:19 UTC
**Lab01-01.dll:** 2010-12-19 16:16:38 UTC
![Screenshot_7](https://github.com/user-attachments/assets/15cd6107-d08f-40c2-ba7d-3334edf9ae92)
![Screenshot_8](https://github.com/user-attachments/assets/1d0e46e6-91b2-497b-826d-25f99cfa74c9)



#### Вопрос 3: Есть ли признаки того, что какой-то из этих файлов запакован или обфусцирован? Если да, то 
#### что это за признаки? 
**Результат:** Признаки упаковки или обфускации отсутствуют

**Доказательства:**
- Низкая энтропия 
- Стандартные имена (.text, .rdata, .data)
  ![Screenshot_9](https://github.com/user-attachments/assets/694d560e-7100-43c3-bf21-28e3ff3e5fb5)
  ![Screenshot_10](https://github.com/user-attachments/assets/99e5d24d-5238-4517-be38-8264a9a98a4a)



#### Вопрос 4: Выдают ли какие-либо импорты функций назначение вредоноса? Если да, то что это за функции?

Да, имеются подозрительные функции

**Lab01-01.exe:**
**FindFirstFileA, FindNextFileA, FindClose , CopyFileA, CreateFileA, CreateFileMappingA, MapViewOfFile** - Работа с файлами, копирование, поиск, сканирование, чтение данных

**Lab01-01.dll:**
**CreateProcessA, CreateMutexA, OpenMutexA, Sleep** - Запуск новых процессов,создание мьютекса, приостановка работы
**socket, connect, send, recv, inet_addr, htons** - Установки сетевого соединения и обмена данными

![Screenshot_11](https://github.com/user-attachments/assets/ea58196d-85de-4364-8d75-efd14036adfa)
![Screenshot_12](https://github.com/user-attachments/assets/815c28b1-b91a-404c-b7f9-c638232ce5e0)


#### Вопрос 5:  Присутствуют ли в системе другие файлы или локальные признаки, которые вы могли бы 
### исследовать? 

**Lab01-01.exe:**
kerne132.dll - подозрительный файл похожий на kernel32.dll. Указан путь к системе C:\windows\system32\kerne132.dll
Lab01-01.dll - указывает на обьединение со 2 файлом
WARNING_THIS_WILL_DESTROY_YOUR_MACHINE - подозрительная надпись

**Lab01-01.dll:**
127.26.152.13 - подозрительный IP
CreateMutexA, OpenMutexA - создание и открытия мьютекса

![Screenshot_13](https://github.com/user-attachments/assets/3499019f-f30a-4bd8-945c-6db76681d00e)
![Screenshot_14](https://github.com/user-attachments/assets/a1549189-aeb6-41fc-adbc-8882a4c7247d)
![Screenshot_15](https://github.com/user-attachments/assets/d073bdc5-1875-4732-9d0f-d52049fe8a10)


### Вопрос 6: С помощью каких сетевых признаков можно обнаружить данную вредоносную программу в 
### зараженной системе? 
Наличие IP аддреса 127.26.152.13 в файле Lab01-01.dll

### Вопрос 7: Как вы думаете, каково назначение этих файлов? 
Lab01-01.exe - Загрузчик.Меняет конфигурацию системы
Lab01-01.dll - Открывает доступ к системе через интернет



