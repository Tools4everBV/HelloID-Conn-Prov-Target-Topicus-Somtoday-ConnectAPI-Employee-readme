# HelloID-Conn-Prov-Target-Topicus-Somtoday-ConnectAPI-Employee-readme

| :warning: Warning - **You need to sign a contract with the supplier before implementing this connector**|
|:---------------------------|
| This repository contains the connector and configuration code only. The implementer is responsible to acquire the connection details such as username, password, certificate, etc. Please contact the client's application manager to coordinate the connector requirements.       |

| :information_source: Contact |
|:---------------------------|
| Please contact your local Tools4ever sales representative for further information and details about the implementation of this connector  |

<br />
<p align="center">
  <img src="assets/logo.png">
</p>

## Table of contents

- [Introduction](#introduction)
- [Getting started](#getting-started)
  + [Connection settings](#connection-settings)
  + [Prerequisites](#prerequisites)
  + [Remarks](#remarks)
- [Setup the connector](#setup-the-connector)
- [Getting help](#getting-help)
- [HelloID Docs](#helloid-docs)

## Introduction

_HelloID-Conn-Prov-Target-Topicus-Somtoday-ConnectAPI-Employee_ is a _target_ connector. Topicus-Somtoday-ConnectAPI provides a set of REST API's that allow you to programmatically interact with it's data. The HelloID connector uses the API endpoints listed in the table below.

| Endpoint     | Description |
| ------------ | ----------- |
| /connect/vestiging/medewerker/account | Updates and retrieves medewerker account information |

## Getting started

### Connection settings

The following settings are required to connect to the API.

| Setting      | Description                                    | Mandatory   |
| ------------ | -----------                                    | ----------- |
| ClientId     | The ClientId to connect to the API             | Yes         |
| ClientSecret | The UserClientSecretName to connect to the API | Yes         |
| Instelling   | The name of the organization in Somtoday       | Yes         |
| BaseUrl      | The URL to the API                             | Yes         |
| IsDebug      | When toggled, debug logging will be displayed  | No          |

### Prerequisites

The connector is created for both HelloID on-premises (using the HelloID agent) and cloud. When running this connector on-premises, make sure to have installed Windows PowerShell 5.1.

### Remarks

- As implementer, you need your own set of credentials before you can implement this connector. Therefore you need to sign a contract with the supplier.

- A School (also knows as an 'organization' within Somtoday) might have multiple departments (or vestigingen). Accounts are correlated based on the value of the 'Organization.Name' in the contract.

- The create.ps1 does not create accounts but merely correlates a HelloID person with an employee in Somtoday.

## Setup the connector

## Getting help

> _For more information on how to configure a HelloID PowerShell connector, please refer to our [documentation](https://docs.helloid.com/hc/en-us/articles/360012558020-Configure-a-custom-PowerShell-target-system) pages_

> _If you need help, feel free to ask questions on our [forum](https://forum.helloid.com)_

## HelloID docs

The official HelloID documentation can be found at: https://docs.helloid.com/
