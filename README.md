# Репортинг (AQA_Exercise_4.1-1)
## Домашнее задание по курсу "Автоматизированное тестирование"
## Тема: «4.1. Репортинг», задание №1: «"Проснулись" (Allure)»
- Интеграция Allure в авто-тесты, использующие Selenide
### Предварительные требования
- На компьютере пользователя должна быть установлена:
	- Intellij IDEA
### Инструкция по интеграции и настройке связки Allure-Selenide
1. В build.gradle прописать:
	```
	plugins {
		...
		id 'io.qameta.allure' version '2.9.6'
	}

	...

	allure {
		version = '2.17.2'
		//Если используется JUnit5, то добавляется:
		useJUnit5 { version = '2.17.2' }
		//версия должна совпадать с версией allure
	}

	repositories {
		mavenCentral()
	}

	dependencies {
		...

		testImplementation 'io.qameta.allure:allure-selenide:2.17.2'

		...
	}
	```	
1. Включить в тестовый класс методы:
	```
	@BeforeAll
    public static void setUpAll() {
        SelenideLogger.addListener("allure", new AllureSelenide());
    }
	```
	```
	@AfterAll
    public static void tearDownAll() {
        SelenideLogger.removeListener("allure");
    }
	```
### Установка и запуск
1. Склонировать проект на свой компьютер
	- открыть терминал
	- ввести команду 
		```
		git clone https://github.com/Lognestix/AQA_Exercise_4.1
		```
1. Открыть склонированный проект в Intellij IDEA
1. В Intellij IDEA перейти во вкладку Terminal (Alt+F12) и запустить SUT командой
	```
	java -jar artifacts/app-card-delivery.jar
	```
1. Запустить авто-тесты В Intellij IDEA во вкладке Terminal открыв еще одну сессию, ввести команду
	```
	./gradlew clean test allureReport
	```
1. В Intellij IDEA во вкладке Terminal ввести команду
	```
	./gradlew allureServe
	```