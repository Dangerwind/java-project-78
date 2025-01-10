### Hexlet tests and linter status:
[![Actions Status](https://github.com/Dangerwind/java-project-78/actions/workflows/hexlet-check.yml/badge.svg)](https://github.com/Dangerwind/java-project-78/actions)
[![Java CI](https://github.com/Dangerwind/java-project-78/actions/workflows/main.yml/badge.svg)](https://github.com/Dangerwind/java-project-78/actions/workflows/main.yml) 
[![Maintainability](https://api.codeclimate.com/v1/badges/db6e54e3c8b342efd107/maintainability)](https://codeclimate.com/github/Dangerwind/java-project-78/maintainability)
[![Test Coverage](https://api.codeclimate.com/v1/badges/db6e54e3c8b342efd107/test_coverage)](https://codeclimate.com/github/Dangerwind/java-project-78/test_coverage)


# Проект **"Валидатор данных"**

Валидатор данных – библиотека, с помощью которой можно проверять корректность любых данных. 
Проверить можно числовые данные, строки и Map с проверкой структуры.

| Название    | Проверка               | применимость        |
|:------------|:-----------------------|:--------------------|
| required()  | на заполненность       | Number, String, Map |
| minLength() | на минимальную длтинну | String, Map         |
| contains()  | на содержание          | String, Map         |
| positive()  | на положительность     | Number              |
| range()     | на диапазон            | Number              |
| sizeof()    | на количество ключей   | Map                 |
| shape()     | для создания схемы     | Map                 |


Пример использования:
```
import hexlet.code.Validator;
import hexlet.code.schemas.StringSchema;
import hexlet.code.schemas.NumberSchema;
import hexlet.code.schemas.MapSchema;
import hexlet.code.schemas.BaseSchema;

Validator v = new Validator();

// Строки
StringSchema schema = v.string().required();

schema.isValid("what does the fox say"); // true
schema.isValid(""); // false

// Числа
NumberSchema schema = v.number().required().positive();

schema.isValid(-10); // false
schema.isValid(10); // true

// Объект Map с поддержкой проверки структуры
Map<String, BaseSchema<String>> schemas = new HashMap<>();
schemas.put("firstName", v.string().required());
schemas.put("lastName", v.string().required().minLength(2));

MapSchema schema = v.map().sizeof(2).shape(schemas);

Map<String, Object> human1 = new HashMap<>();
human1.put("firstName", "John");
human1.put("lastName", "Smith");
schema.isValid(human1); // true

Map<String, Object> human2 = new HashMap<>();
human2.put("firstName", "Anna");
human2.put("lastName", "B");
schema.isValid(human2); // false
```

