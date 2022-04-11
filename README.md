# Eltex.Course3

## 6-7-10:
Самостоятельное написание, компиляция и запуск программы для организации связи двух процессов через разделяемую память.

Для закрепления полученных знаний напишите две программы, осуществляющие взаимодействие через разделяемую память. Первая программа должна создавать сегмент разделяемой памяти и копировать туда свой собственный исходный текст, вторая программа должна брать оттуда этот текст, печатать его на экране и удалять сегмент разделяемой памяти из системы.

## 8-7:
Написание, компиляция и прогон программы с организацией взаимоисключения с помощью семафоров для 2-х процессов, взаимодействующих через разделяемую память.

На прошлом занятии мы установили, что любые неатомарные операции, связанные с изменением содержимого разделяемой памяти, представляют собой критическую секцию процесса или нити исполнения. Модифицируйте программы /ftp/pub/sem6-7/stud/06-3a.c и /ftp/pub/sem6-7/stud/06-3b.c, которые иллюстрировали некорректную работу через разделяемую память, обеспечив с помощью семафоров взаимоисключения для их правильной работы.

## 9-10:
Используя технику из предыдущего примера, мы можем организовать получение сообщений одним процессом от множества других процессов через одну очередь сообщений и отправку им ответов через ту же очередь сообщений, т.е. осуществить мультиплексирование сообщений. Вообще под мультиплексированием информации понимают возможность одновременного обмена информацией с несколькими партнерами. Метод мультиплексирования широко применяется в модели взаимодействия процессов клиент-сервер. В этой модели один из процессов является сервером. Сервер получает запросы от других процессов - клиентов - на выполнение некоторых действий и отправляет им результаты обработки запросов. Наиболее часто модель клиент-сервер используется при разработке сетевых приложений, с которыми мы столкнемся на завершающих семинарах курса. Она изначально предполагает неравноправность взаимодействующих процессов:
Сервер, как правило, работает постоянно, на всем протяжении жизни приложения, а клиенты могут работать эпизодически.
Сервер ждет запроса от клиентов, инициатором же взаимодействия выступает клиент.
Как правило, клиент обращается к одному серверу за раз, в то время как к серверу могут одновременно поступить запросы от нескольких клиентов.
Клиент должен знать, как обратиться к серверу (например, какого типа сообщения он воспринимает) перед началом организации запроса к серверу, в то время как сервер может получить недостающую информацию о клиенте из пришедшего запроса.
Рассмотрим следующую схему мультиплексирования сообщений через одну очередь сообщений для модели клиент-сервер. Пусть сервер получает из очереди сообщений только сообщения с типом 1. В состав сообщений с типом 1, посылаемых серверу, процессы-клиенты включают значение своих идентификаторов процесса. Приняв сообщение с типом 1, сервер анализирует его содержание, выявляет идентификатор процесса, пославшего запрос, и отвечает клиенту, посылая сообщение с типом равным идентификатору запрашивавшего процесса. Процесс-клиент после посылки запроса ожидает ответа в виде сообщения с типом равным своему идентификатору. Поскольку идентификаторы процессов в системе различны, и ни один пользовательский процесс не может иметь PID равный 1, все сообщения могут быть прочитаны только теми процессами, которым они адресованы. Если обработка запроса занимает продолжительное время, сервер может организовывать параллельную обработку запросов, порождая для каждого запроса новый процесс-ребенок или новую нить исполнения.

Написание, компиляция и прогон программ клиент и сервер.
Напишите, откомпилируйте и прогоните программы сервера и клиентов для предложенной схемы мультиплексирования сообщений.

## 10:
В приведенном выше примере сервер осуществлял последовательную обработку запросов от разных клиентов. При таком подходе клиенты могут подолгу простаивать после установления соединения, ожидая обслуживания. Поэтому обычно применяется схема псевдопараллельной обработки запросов. После приема установленного соединения сервер порождает процесс-ребенок, которому и поручает дальнейшую работу с клиентом. Процесс-родитель закрывает присоединенный сокет и уходит на ожидание нового соединения. Схематично организация такого сервера изображена на рис. 15–16.9.

Напишите, откомпилируйте и запустите такой параллельный сервер. Убедитесь в его работоспособности. Не забудьте о необходимости удаления зомби-процессов.
