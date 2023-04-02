# Postman_HW_3

1. Необходимо залогиниться
```
request: POST
http://162.55.220.72:5005/login
login: str
password: str
```
Приходящий токен необходимо передать во все остальные запросы.

Дальше все запросы требуют наличие токена.

2. http://162.55.220.72:5005/user_info
```
request: POST (RAW JSON)
age: int
salary: int
name: str
auth_token
```
```
response:
{'start_qa_salary': salary,
 'qa_salary_after_6_months': salary * 2,
 'qa_salary_after_12_months': salary * 2.9,
 'person': {'u_name':[user_name, salary, age],
            'u_age':age,
            'u_salary_1.5_year': salary * 4}
}
```
Тесты:
- Статус код 200
- Проверка структуры json в ответе
- В ответе указаны коэффициенты умножения `salary`, напишите тесты по проверке правильности результата перемножения на коэффициент
- Достать значение из поля `u_salary_1.5_year` и передать в поле `salary` запроса `http://162.55.220.72:5005/get_test_user`

3. http://162.55.220.72:5005/new_data
```
request: POST
age: int
salary: int
name: str
auth_token
```
```
response:
{'name': name,
 'age': int(age),
 'salary': [salary, str(salary*2), str(salary*3)]
}
```
Тесты:
- Статус код 200
- Проверка структуры json в ответе
- В ответе указаны коэффициенты умножения `salary`, напишите тесты по проверке правильности результата перемножения на коэффициент
- Проверить, что 2-й элемент массива `salary` больше 1-го и 0-го

4. http://162.55.220.72:5005/test_pet_info
```
request: POST
age: int
weight: int
name: str
auth_token
```
```
response:
{'name': name,
 'age': age,
 'daily_food': weight * 0.012,
 'daily_sleep': weight * 2.5
}
```
Тесты:
- Статус код 200
- Проверка структуры json в ответе
- В ответе указаны коэффициенты умножения `weight`, напишите тесты по проверке правильности результата перемножения на коэффициент

5. http://162.55.220.72:5005/get_test_user
```
request: POST
age: int
salary: int
name: str
auth_token
```
```
response:
{'name': name,
 'age': age,
 'salary': salary,
 'family': {'children':[['Alex', 24],['Kate', 12]],
            'u_salary_1.5_year': salary * 4}
}
```
Тесты:
- Статус код 200
- Проверка структуры json в ответе
- Проверить, что значение поля `name` равно значению переменной `name` из окружения
- Проверить, что значение поля `age` в ответе соответсвует отправленному в запросе значению поля `age`

6. http://54.157.99.22:80/currency
```
request: POST
auth_token
```
```
response: Передаётся список массив объектов
[{"Cur_Abbreviation": str,
  "Cur_ID": int,
  "Cur_Name": str
 }
 …
 {"Cur_Abbreviation": str,
  "Cur_ID": int,
  "Cur_Name": str
 }]
```
Тесты:
- Можете взять любой объект из присланного списка, используйте js random. В объекте возьмите `Cur_ID` и передать через окружение в следующий запрос.

7. http://54.157.99.22:80/curr_byn
```
request: POST
auth_token
curr_code: int
```
```
response:
{"Cur_Abbreviation": str
 "Cur_ID": int,
 "Cur_Name": str,
 "Cur_OfficialRate": float,
 "Cur_Scale": int,
 "Date": str
}
```
Тесты:
- Статус код 200
- Проверка структуры json в ответе

Задание со * 6 и 7:
1) получить список валют
2) итерировать список валют
3) в каждой итерации отправлять запрос на сервер для получения курса каждой валюты
4) если возвращается 500 код, переходим к следующей итреации
5) если получаем 200 код, проверяем response json на наличие поля `Cur_OfficialRate`
6) если поле есть, пишем в консоль инфу про валюту в виде response:
```
	{
    	"Cur_Abbreviation": str
    	"Cur_ID": int,
    	"Cur_Name": str,
    	"Cur_OfficialRate": float,
    	"Cur_Scale": int,
    	"Date": str
	}
 ```
7) переходим к следующей итерации
