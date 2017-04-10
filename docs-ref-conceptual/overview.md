---
title: Azure CLI 2.0
description: Overview of the Azure CLI 2.0.
keywords: Azure CLI 2.0, Linux, Mac, Windows, OS X, Ubuntu, Debian, CentOS, RHEL, SUSE, CoreOS, Docker, Windows, Python, PIP
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 02/27/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: azurecli
ms.service: multiple
ms.assetid: 80ae9f6c-adb7-483c-bfb4-fbb958e075ba
---

# Azure CLI 2.0

Azure CLI 2.0은 Azure 자원을 관리하기 위한 새로운 명령어 라인 경험을 제공합니다. macOS, Linux, 그리고 Windows에서 사용 가능합니다.

Azure CLI 2.0은 명령어 라인에서 Azure 자원 관리 및 Azure 리소스 관리자에 대한 작업을 자동화하는 스크립트를 만드는데 최적화되어 있습니다. Azure CLI 2.0을 사용하면 다음 명령어를 입력하여 Azure 내 가상 컴퓨터를 쉽게 생성할 수 있습니다:

```azurecli
az vm create -n MyLinuxVM -g MyResourceGroup --image UbuntuLTS
```

[Install article](install-azure-cli.md) 를 살펴보고 Azure CLI 2.0를 가져와 시스템에 실행하십시오. 그리고 나서, 사용해 보기 위해 [Get Started](get-started-with-azure-cli.md) 게시글을 읽어 봅니다.
최신 릴리즈에 대한 정보는, [release notes](release-notes-azure-cli.md)를 살펴봅니다.

다음 예제는 Azure CLI 2.0을 기반으로 하는 일반적인 시나리오를 학습할 수 있도록 도와줄 것입니다:
- [Linux Virtual Machines](/azure/virtual-machines/virtual-machines-linux-cli-samples?toc=%2fcli%2fazure%2ftoc.json&bc=%2fcli%2fazure%2fbreadcrumb%2ftoc.json)
- [Windows Virtual Machines](/azure/virtual-machines/virtual-machines-windows-cli-samples?toc=%2fcli%2fazure%2ftoc.json&bc=%2fcli%2fazure%2fbreadcrumb%2ftoc.json)
- [Web Apps](/azure/app-service-web/app-service-cli-samples?toc=%2fcli%2fazure%2ftoc.json&bc=%2fcli%2fazure%2fbreadcrumb%2ftoc.json)
- [SQL Database](/azure/sql-database/sql-database-cli-samples?toc=%2fcli%2fazure%2ftoc.json&bc=%2fcli%2fazure%2fbreadcrumb%2ftoc.json)

개별 Azure CLI 2.0 명령어를 사용하는 방법을 문서화한 자세한 [레퍼런스](/cli/azure/) 또한 확인 가능합니다.

Azure CLI 2.0을 지금 [시작해 보세요](get-started-with-azure-cli.md).


> [!NOTE]
> 이전 버전의 CLI (Azure CLI)를 사용하는 경우, 해당 버전을 계속해서 사용 가능합니다.
> 두 CLI를 사용하는 경우 `azure` 는 이전 CLI - Azure CLI 이며, `az` 는 새로운 CLI인 Azure CLI 2.0 임을 기억합니다.
