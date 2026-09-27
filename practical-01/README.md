# Практична робота №1

## Створення та розгортання SAP Fiori застосунків у SAP Business Technology Platform

## Мета роботи

Ознайомитися з основними етапами розробки та розгортання хмарних застосунків у **SAP Business Technology Platform (SAP BTP)**, отримати практичні навички роботи з **SAP Business Application Studio**, **SAP Fiori tools**, **Git/GitHub**, **CI/CD**, **SAP Build Work Zone**, а також створити SAP Fiori Elements застосунок на основі зовнішнього OData-сервісу.

У межах практичної роботи необхідно:

1. частково виконати SAP Mission зі створення SAP Fiori застосунку;
2. створити та запустити тестовий застосунок **Hello World**;
3. налаштувати роботу з Git та GitHub;
4. ознайомитися з процесом CI/CD та розгортання застосунку в SAP BTP;
5. опублікувати застосунок у **SAP Build Work Zone**;
6. створити власний SAP Fiori Elements застосунок **Suppliers**;
7. підключити застосунок до публічного OData-сервісу **Northwind**;
8. налаштувати представлення даних за допомогою OData-анотацій;
9. виконати build та deploy застосунку Suppliers;
10. додати Suppliers до SAP Build Work Zone.

---

## Загальна схема виконання практичної роботи

Практична робота складається з двох основних частин.

### Частина 1. SAP Mission та Hello World

У першій частині використовується SAP Mission, за допомогою якої необхідно ознайомитися з типовим життєвим циклом SAP BTP застосунку:

**SAP BTP Trial → SAP Business Application Studio → Hello World → Git/GitHub → CI/CD → Deploy → SAP Build Work Zone**

У результаті в SAP Build Work Zone повинен бути доступний застосунок **Hello World**.

### Частина 2. Створення Suppliers

У другій частині необхідно самостійно створити SAP Fiori Elements застосунок, який використовує публічний OData-сервіс Northwind.

Застосунок повинен забезпечувати:

- перегляд списку постачальників;
- фільтрацію постачальників;
- перехід до сторінки окремого постачальника;
- перегляд контактної інформації та адреси постачальника;
- перегляд товарів постачальника;
- перехід до сторінки окремого товару.

---

# 1. Частина 1. SAP Mission та Hello World

## 1.1. Виконання SAP Mission

Для виконання першої частини практичної роботи використовується SAP Mission:

**Set Up SAP BTP for Fiori/SAPUI5 and create a Hello World app**

[SAP Mission — перейти до виконання](https://discovery-center.cloud.sap/protected/index.html#/mymissiondetail/125910/?tab=overview)

> **Важливо:** проходити всю SAP Mission не потрібно. У межах практичної роботи необхідно виконати лише зазначені нижче етапи.

Необхідно опрацювати такі частини Mission:

1. **Discover**
2. **Setup Trial Account for HTML5 Development**
3. **Create an App in Business Application**
4. **Set Up Additional Features**

Під час виконання Mission звертайте увагу не лише на послідовність дій, а й на призначення сервісів SAP BTP, які використовуються для створення, розгортання та публікації застосунку.

---

## 1.2. Підготовка SAP BTP Trial

Виконайте етап:

**Setup Trial Account for HTML5 Development**

Переконайтеся, що SAP BTP Trial Account підготовлений для HTML5-розробки та доступні необхідні сервіси.

Для подальшої роботи необхідно мати доступ до:

- Cloud Identity Services;
- Continuous Integration & Delivery;
- SAP Business Application Studio;
- Cloud Foundry environment;
- SAP Build Work Zone, standard edition.

---

## 1.3. Створення Hello World

Перейдіть до етапу Mission:

**Create an App in Business Application Studio**

Відкрийте **SAP Business Application Studio** та виконайте кроки Mission зі створення тестового застосунку.

> Результатом цього етапу повинен бути працездатний застосунок **Hello World**, запущений із SAP Business Application Studio та з SAP Build Work Zone.

---

## 1.4. Налаштування Git/GitHub та CI/CD

Перейдіть до етапу Mission:

**Set Up Additional Features**

Виконайте два кроки:

1. **Enable Git and Add a Remote Repository** — налаштуйте Git для проєкту та підключіть віддалений репозиторій GitHub.
2. **Setup Continuous Integration and Delivery Service CI/CD** — налаштуйте CI/CD для автоматичного збирання та розгортання застосунку.

> **Примітка:** у SAP Mission ці кроки позначені як *Optional*, однак у межах практичної роботи їх виконання є обов'язковим.

---

# 2. Частина 2. Створення Suppliers

## 2.1. Створення Destination у SAP BTP

Для доступу до зовнішнього OData-сервісу необхідно створити Destination у SAP BTP.

У SAP BTP Cockpit відкрийте:

**Connectivity → Destinations**

та створіть новий Destination з такими параметрами:

| Параметр | Значення |
|---|---|
| Name | `Northwind` |
| Type | `HTTP` |
| Description | `Northwind` |
| URL | `https://services.odata.org/` |
| Proxy Type | `Internet` |
| Authentication | `NoAuthentication` |

Додайте такі **Additional Properties**:

| Property | Value |
|---|---|
| `HTML5.DynamicDestination` | `True` |
| `HTML5.Timeout` | `60000` |
| `WebIDEUsage` | `odata_gen` |
| `WebIDEEnabled` | `true` |
| `MobileEnabled` | `True` |
| `usage` | `Backend` |

> **Важливо:** у полі `URL` необхідно вказати лише базову адресу `https://services.odata.org/`. Шлях до конкретного OData-сервісу буде задано пізніше в SAP Fiori generator.

Збережіть Destination.

<!-- SCREENSHOT 01: Northwind Destination -->

Після збереження можна скористатися кнопкою **Check Connection** для перевірки доступності сервісу.

---

## 2.2. Створення SAP Fiori Elements застосунку

Відкрийте **SAP Business Application Studio** та запустіть створення нового проєкту:

**File → New Project from Template**

<!-- SCREENSHOT 02: File → New Project from Template -->

Оберіть:

**SAP Fiori generator**

і перейдіть до наступного кроку.

Як шаблон застосунку виберіть:

**List Report Page**

---

## 2.3. Підключення OData-сервісу

На кроці **Data Source and Service Selection** встановіть:

**Data Source:**

```text

Connect to a System

```

**System:**

```text

Northwind

```

У полі **Service Path** введіть:

```text

V3/Northwind/Northwind.svc/

```

Після завантаження метаданих виберіть сервіс:

```text

https://services.odata.org/V3/Northwind/Northwind.svc/

```

<!-- SCREENSHOT 03: Data Source and Service Selection -->

> **Важливо:** у цій практичній роботі використовується саме **Northwind OData V3**:

>

> ```text

> V3/Northwind/Northwind.svc/

> ```

>

> Не використовуйте `V4/Northwind/Northwind.svc/`.

Натисніть **Next**.

---

## 2.4. Вибір сутностей

На кроці **Entity Selection** встановіть:

| Параметр | Значення |
|---|---|
| Main Entity | `Suppliers` |
| Navigation Entity | `Products` |
| Table Type | `Responsive` |

<!-- SCREENSHOT 04: Entity Selection -->

Таким чином, основною сутністю застосунку будуть постачальники (`Suppliers`), а з Object Page постачальника можна буде перейти до пов'язаних з ним товарів (`Products`).

Натисніть **Next**.

---
