# Хмарні та грід-технології

Репозиторій містить матеріали та інструкції до практичних робіт з дисципліни  
**«Хмарні та грід-технології»**.

## Практичні роботи

### Практична робота №1
**Створення та розгортання SAP Fiori застосунків у SAP Business Technology Platform**

У практичній роботі розглядається:

- підготовка середовища **SAP BTP Trial** для HTML5-розробки;
- створення тестового застосунку **Hello World** у SAP Business Application Studio;
- робота з **Git та GitHub**;
- налаштування **CI/CD** та розгортання застосунку в SAP BTP;
- публікація застосунку в **SAP Build Work Zone**;
- створення власного SAP Fiori Elements застосунку **Suppliers**;
- підключення до публічного OData-сервісу **Northwind**;
- налаштування **List Report** та **Object Page** за допомогою OData-анотацій;
- робота з пов'язаними сутностями **Suppliers** та **Products**;
- розгортання та публікація застосунку **Suppliers** у SAP Build Work Zone.

[Перейти до практичної роботи №1](./practical-01/README.md)

---

### Практична робота №2

**Інтеграція хмарних застосунків за допомогою SAP Integration Suite**

У практичній роботі розглядається:

- активація та налаштування SAP Integration Suite;
- створення та розгортання Integration Flow;
- надсилання повідомлень у SAP Build Work Zone;
- формування відповідей у форматах JSON та XML;
- налаштування автоматичного запуску Integration Flow за розкладом.

[Перейти до практичної роботи №2](practical-02/README.md)

---

### Практична робота №3

**Створення мультитенантного SaaS-застосунку в SAP BTP**

У практичній роботі розглядається:

- перетворення SAPUI5-застосунку Hello World на мультитенантний SaaS-застосунок;
- розгортання SaaS-застосунку в субакаунті Provider;
- створення Consumer-субакаунта та оформлення підписки на SaaS-застосунок;
- налаштування SAP Build Work Zone, standard edition у Consumer-субакаунті;
- створення плитки для запуску SaaS-застосунку через SAP Build Work Zone.

[Перейти до практичної роботи №3](practical-03/README.md)

## Необхідне середовище

Для виконання практичних робіт використовується:

- SAP BTP;
- SAP Business Application Studio;
- SAP Build Work Zone;
- Cloud Foundry Environment;
- SAP Fiori tools;
- Git / GitHub.

## Структура репозиторію

```text
cloud-grid-technologies-2026/
│
├── README.md
│
├── practical-01/
│   ├── README.md
│   ├── resources/
│   │   ├── destination.json
│   │   └── annotation.xml
│   └── images/
│
├── practical-02/
│   ├── README.md
│   ├── resources/
│   └── images/
│
└── practical-03/
    ├── README.md
    ├── resources/
    └── images/
