# devops-netology_4.3  
Домашнее задание к занятию "4.3. Языки разметки JSON и YAML"
Обязательная задача 1

Мы выгрузили JSON, который получили через API запрос к нашему сервису:

    { "info" : "Sample JSON output from our service\t",
        "elements" :[
            { "name" : "first",
            "type" : "server",
            "ip" : 7175 
            }
            { "name" : "second",
            "type" : "proxy",
            "ip : 71.78.22.43
            }
        ]
    }

Нужно найти и исправить все ошибки, которые допускает наш сервис

    {
    	"info": "Sample JSON output from our service\t",
    	"elements": [
    	{
    		"name": "first",
    		"type": "server",
    		"ip": 7175
    	},
    	{
    		"name": "second",
    		"type": "proxy",
    		"ip": "71.78 .22 .43"
    	}]
    }

Обязательная задача 2

В прошлый рабочий день мы создавали скрипт, позволяющий опрашивать веб-сервисы и получать их IP. К уже реализованному функционалу нам нужно добавить возможность записи JSON и YAML файлов, описывающих наши сервисы. Формат записи JSON по одному сервису: { "имя сервиса" : "его IP"}. Формат записи YAML по одному сервису: - имя сервиса: его IP. Если в момент исполнения скрипта меняется IP у сервиса - он должен так же поменяться в yml и json файле.
Ваш скрипт:

    jdata="data.json"
    ydata="data.yaml"
    n = 0
    addr = {"drive.google.com": socket.gethostbyname("drive.google.com"),
       "mail.google.com": socket.gethostbyname("mail.google.com"),
        "google.com": socket.gethostbyname("google.com")}
    while n < 1:
        n = n + 1
        for host in addr:
            if addr[host] != socket.gethostbyname(host):
                print("[ERROR] " + str(host) + " IP mismatch: " + addr[host] + "--- " + socket.gethostbyname(host))
            addr[host] = socket.gethostbyname(host)
            print(host + " --- " + addr[host] + " OK")
            with open(jdata, "w") as dataj:
                json.dump(addr, dataj, indent=2)
            with open(ydata, "w") as datay:
                datay.write(yaml.dump(addr, explicit_start=True, explicit_end=True))



Вывод скрипта при запуске при тестировании:

    drive.google.com --- 142.251.1.194 OK
    mail.google.com --- 216.58.207.197 OK
    google.com --- 142.250.74.78 OK


json-файл(ы), который(е) записал ваш скрипт:

    {
      "drive.google.com": "142.251.1.194",
      "mail.google.com": "216.58.207.197",
      "google.com": "142.250.74.78"
    }

yml-файл(ы), который(е) записал ваш скрипт:

    ---
    drive.google.com: 142.251.1.194
    google.com: 142.250.74.78
    mail.google.com: 216.58.207.197
    ...

