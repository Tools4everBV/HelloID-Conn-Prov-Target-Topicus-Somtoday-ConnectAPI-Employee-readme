# HelloID-Conn-Prov-Target-Topicus-Somtoday-ConnectAPI-Employee-Readme

> [!IMPORTANT]
> This repository contains the connector and configuration code only. The implementer is responsible to acquire the connection details such as username, password, certificate, etc. You might even need to sign a contract or agreement with the supplier before implementing this connector. Please contact the client's application manager to coordinate the connector requirements.

|:---------------------------|
| This is a private repository due to need for own credentials as implementor for this connector (or the usage of our internal credential proxy) |

> :warning: Warning - **You need to sign a contract with the supplier before implementing this connector*


<br />
<p align="center">
  <img src="assets/logo.png">
</p>

## Table of contents

- [HelloID-Conn-Prov-Target-Topicus-Somtoday-ConnectAPI-Employee-Readme](#helloid-conn-prov-target-topicus-somtoday-connectapi-employee-readme)
  - [Table of contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Getting started](#getting-started)
    - [Prerequisites](#prerequisites)
    - [Connection settings](#connection-settings)
    - [Correlation configuration](#correlation-configuration)
    - [Available lifecycle actions](#available-lifecycle-actions)
    - [Field mapping](#field-mapping)
  - [Remarks](#remarks)
    - [Supplier credentials](#supplier-credentials)
    - [Organizations (\_setting.currentSchoolName)](#organizations-_settingcurrentschoolname)
    - [Create.ps1 only correlate](#createps1-only-correlate)
    - [HR target Source](#hr-target-source)
    - [Employee vs Account](#employee-vs-account)
    - [Change School](#change-school)
  - [Development resources](#development-resources)
    - [API endpoints](#api-endpoints)
    - [API documentation](#api-documentation)
  - [Getting help](#getting-help)
  - [HelloID docs](#helloid-docs)

## Introduction

_HelloID-Conn-Prov-Target-Topicus-Somtoday-ConnectAPI-Employee_ is a _target_ connector. _Topicus-Somtoday-ConnectAPI-Employee_ provides a set of REST API's that allow you to programmatically interact with its data.

## Getting started

### Prerequisites
- **CustomProperty**:<br>
- When using Somtoday Source, you need a custom property in your system to save the UUID of the employee, so you can use the UUID as the correlation key. *More information can be find here [HelloID Docs](https://docs.helloid.com/en/provisioning/persons/person-schema/add-a-custom-person-or-contract-field.html)*
-
### Connection settings

The following settings are required to connect to the API.

| Setting      | Description                                    | Mandatory |
| ------------ | ---------------------------------------------- | --------- |
| ClientId     | The ClientId to connect to the API             | Yes       |
| ClientSecret | The UserClientSecretName to connect to the API | Yes       |
| Instelling   | The name of the organization in SomToday       | Yes       |
| BaseUrl      | The URL to the API                             | Yes       |
| TokenUrl     | The Token URL to the API                       | Yes       |




### Correlation configuration

The correlation configuration is used to specify which properties will be used to match an existing account within _Topicus-Somtoday-ConnectAPI-Employee_ to a person in _HelloID_.

| Setting                   | Value                 |
| ------------------------- | --------------------- |
| Enable correlation        | `True`                |
| Person correlation field  | `Custom.SomTodayUUID` |
| Account correlation field | `uuid`                |

> More information about `UUID` correlation in section: [HR target Source](#hr-target-source)

> [!TIP]
> _For more information on correlation, please refer to our correlation [documentation](https://docs.helloid.com/en/provisioning/target-systems/powershell-v2-target-systems/correlation.html) pages_.

### Available lifecycle actions

The following lifecycle actions are available:

| Action             | Description                                                                     |
| ------------------ | ------------------------------------------------------------------------------- |
| create.ps1         | Correlates existing Employees                                                   |
| update.ps1         | Create/Updates accounts for the Employee, and updates the properties            |
| configuration.json | Contains the connection settings and general configuration for the connector.   |
| fieldMapping.json  | Defines mappings between person fields and target system person account fields. |

### Field mapping

The field mapping can be imported by using the _fieldMapping.json_ file.

## Remarks
### Supplier credentials
As implementer, you need your own set of credentials before you can implement this connector. Therefore you need to sign a contract with the supplier.

### Organizations (_setting.currentSchoolName)
A School (also knows as an 'organization' within Somtoday) might have multiple departments (or vestigingen). Accounts are correlated based on the value of the '_setting.currentSchoolName' in the fieldMapping.

### Create.ps1 only correlate
The create.ps1 does not create accounts but merely correlates a HelloID person with an employee in Somtoday.

### HR target Source
Since this connector is often used with the Somtoday Source connector, the current version uses the employee's UUID -with a custom property- to correlate the account in Somtoday. However, the connector can be used with other source systems. To achieve this, you should add a field in the field mapping and use it as the correlation key or value. This should be an existing property in Somtoday. For example, `externnummer` or `medewerkernummer`.

### Employee vs Account
The connector manages the accounts of employees in Somtoday. Therefore, it does not create or update employee records but only creates accounts for existing employees. The Update action also creates an account if one does not already exist.

### Change School
Currently, it is not supported in the connector for a Somtoday employee to switch between schools. If this is a common situation, it can be implemented, but it requires some modifications to the code. For example, the AccountReference needs to be updated when a school change occurs. If this happens only occasionally, you could remove the account from HelloID and re-run the creation script.


## Development resources

### API endpoints

The following endpoints are used by the connector

| Endpoint                                                             | Description                                                  |
| -------------------------------------------------------------------- | ------------------------------------------------------------ |
| <TokenURL>/oauth2/token?organisation=<organisationId>                | Retrieves the oAuth token                                    |
| /rest/v1/connect/vestiging                                           | Retrieves organizations for which the token is authenticated |
| /rest/v1/connect/vestiging/<VestigingUUID>/medewerker                | Retrieves all employees for a specific department             |
| /rest/v1/connect/vestiging/<VestigingUUID>/medewerker/<uuid>/account | Updates and retrieves Account information                    |


### API documentation
[Swagger Documentation](https://editor.swagger.io/?url=https://api.somtoday.nl/rest/v1/connect/documented/openapi)

## Getting help

> [!TIP]
> _For more information on how to configure a HelloID PowerShell connector, please refer to our [documentation](https://docs.helloid.com/en/provisioning/target-systems/powershell-v2-target-systems.html) pages_.

> [!TIP]
>  _If you need help, feel free to ask questions on our [forum](https://forum.helloid.com/forum/helloid-connectors/provisioning/712-helloid-provisioning-target-somtoday-connectapi-employee)_.

## HelloID docs

The official HelloID documentation can be found at: https://docs.helloid.com/
