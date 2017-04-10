---
title: Get started with Azure CLI 2.0
description: Get started with Azure CLI 2.0 on Linux, Mac, or Windows.
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
ms.assetid: 85c418a8-6177-4833-bb8d-ff4ce2233c1a
---

# Azure CLI 2.0와 함께 시작해보기

Azure CLI 2.0은 Azure 자원을 관리하기 위한 새로운 명령어 라인 경험을 제공합니다. macOS, Linux, 그리고 Windows에서 사용 가능합니다.

Azure CLI 2.0은 명령어 라인에서 Azure 자원 관리 및 Azure 리소스 관리자에 대한 작
업을 자동화하는 스크립트를 만드는데 최적화되어 있습니다.

이 글에서는 시작해 보는 것을 도와주며, 내부적인 핵심 개념을 가르쳐줄 것입니다.

최신 릴리즈에 대한 정보는, [릴리즈 노트](release-notes-azure-cli.md) 를 살펴봅니다.

## Azure CLI 설치

첫 단계에서는 최신 버전의 Azure CLI를 설치하였는가를 살펴보는 것입니다:

1. [Azure CLI 2.0 설치](install-azure-cli.md)
플랫폼은 사용하는 어떤 것이든 관계없습니다.

2. 설치가 성공적이었는지를 검증하기 위해, 명령어 라인에서 `az --version` 를 실행합니다.

Azure CLI 및 대상 컴퓨터에 설치된 다른 의존성 라이브러리 버전 번호를 살펴볼 수 있을 것입니다.

오류가 발생한 경우, CLI를 설치하면서 문제가 발생했을 가능성이 높습니다. [Azure CLI 2.0 설치 글](install-azure-cli.md#troubleshooting) 에서 "설치 트러블슈팅" 섹션을 살펴보거나,
도움을 위해 페이지 하단에 있는 토론에서 댓글을 게시합니다.

## Azure에 로그인

이제 Azure CLI 2.0이 설치되어 있는 상황에서, 다음 단계로는 Azure 계정을 사용하여 안전하게 연결하는 것입니다. 이를 위해서는 `az login` 명령어를 사용합니다.

1. 다음 명령어를 명령어 라인에서 실행합니다.

   ```azurecli
   az login
   ```
   
   다음 단계에서 사용할 코드가 출력될 것입니다.

2. 웹 브라우저를 사용하여 [https://aka.ms/devicelogin](https://aka.ms/devicelogin) 페이지를 연 후 해당 코드를 입력합니다.
  
3. 프롬프트에서 Azure 자격증명을 사용한 로그인이 이루어집니다.

이제 여러분 계정에서 사용 가능한 Azure 자원 및 서비스에 대해 Azure CLI 2.0에서 명령어 실행이 가능합니다.

## 리소스 그룹 생성

이제 모든 것이 셋업되었으므로, Azure CLI 를 사용하여 Azure 내 자원을 생성해 봅시다.

먼저, 리소스 그룹을 생성해 봅시다. Azure에서 리소스 그룹은 논리적으로 서로 묶고자 하는 여러 자원을 관리하는 방법을
제공합니다. 예를 들어, 특정 어플리케이션 또는 프로젝트에 대한  리소스 그룹을 생성하여
가상 컴퓨터, 데이터베이스 및 내부에 CDN 서비스를 생성할 수 있습니다.

Azure에서 *westus2* 지역에 "MyResourceGroup" 이름으로 리소스 그룹을 생성해 봅시다. 이를 위해 다음 명령어를 입력합니다:

```azurecli
az group create -n MyResourceGroup -l westus2 
```

리소스 그룹이 생성된 이후, `az group create` 명령어는 새로 생성된 자원에 대한 몇몇 속성을 출력할 것입니다:

```Output
{
  "id": "/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/MyResourceGroup",
  "location": "westus2",
  "managedBy": null,
  "name": "MyResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## Linux 가상 컴퓨터 생성하기

이제 리소스 그룹이 있는 상황에서, 해당 리소스 그룹 내 Linux VM을 생성해 봅시다.

다음 명령어를 사용하여 10GB 및 20GB 2개의 스토리지 디스크를 연결하여 대중적인 UbuntuLTS 이미지를 사용해 Linux VM을 생성할 수 있습니다:

```azurecli
az vm create -n MyLinuxVM -g MyResourceGroup --image UbuntuLTS --data-disk-sizes-gb 10 20
```

해당 명령어를 실행하면, Azure CLI 2.0는 ~/.ssh 디렉토리 내 저장된 SSH 키페어를 찾습니다. SSH 키페어를 아직 저장하지 않은 경우에는, Azure CLI가 자동으로 생성하도록 요청하기 위해 --generate-ssh-keys 매개변수를 전달할 수 있습니다:

```azurecli
az vm create -n MyLinuxVM -g MyResourceGroup --image UbuntuLTS --generate-ssh-keys
```

`az vm create` 명령어는 VM이 완전히 생성된 후 액세스 및 사용 준비가 되었을 때 출력을 반환합니다. 출력에는 공용 IP 주소를 포함하여 새로 생성된 VM에 대한 몇 가지 속성을 포함합니다.

```Output
{
  "fqdns": "",
  "id": "/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyLinuxVM",
  "location": "westus2",
  "macAddress": "xx-xx-xx-xx-xx-xx",
  "powerState": "VM running",
  "privateIpAddress": "xx.x.x.x",
  "publicIpAddress": "xx.xxx.xxx.xx",
  "resourceGroup": "MyResourceGroup"
}
```

이제 VM이 생성되었습니다. 생성한 VM에 대한 공용 IP 주소를 가지고 **SSH** 를 사용해 새로운 Linux VM에 로그인할 수 있습니다.

```azurecli
ssh xx.xxx.xxx.xxx
```

```Output
Welcome to Ubuntu 14.04.4 LTS (GNU/Linux 3.19.0-65-generic x86_64)

 * Documentation:  https://help.ubuntu.com/

  System information as of Sun Feb 19 00:32:28 UTC 2017

  System load: 0.31              Memory usage: 3%   Processes:       89
  Usage of /:  39.6% of 1.94GB   Swap usage:   0%   Users logged in: 0

  Graph this data and manage this system at:
    https://landscape.canonical.com/

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

my-login@MyLinuxVM:~$
```

## Windows Server 가상 컴퓨터 생성하기

이제 `az vm create` 명령어를 사용해 Windows Server 2016 Datacenter 기반 VM을 생성한 후, Linux VM에서 사용했던 "MyResourceGroup" 리소스 그룹에 추가해 봅시다. Linux VM 예제에서와 같이 `--data-disk-sizes-gb` 매개변수를 사용하여 2개의 스토리지 디스크를 연결할 것입니다.

Azure는 쉽게 추측 가능한 사용자 이름 / 암호를 사용하지 않는 것을 요구 사항으로 하고 있습니다. 사용자 이름 및 암호 모두에 대한 최소 길이 뿐만 아니라 어떤 문자를 사용해야 하는지에 대한 구체적인 규칙이 있습니다.

> [!NOTE]
> 해당 명령어를 실행할 때 사용자 이름 및 암호를 입력하는 프롬프트가 나타날 것입니다.

```azurecli
az vm create -n MyWinVM -g MyResourceGroup --image Win2016Datacenter
```

해당 VM이 완전히 생성된 후 액세스 및 사용 준비가 된 이후 `az vm create` 명령어 출력 결과가 보일 것입니다.

```Output
{
  "fqdns": "",
  "id": "/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWinVM",
  "location": "westus2",
  "macAddress": "xx-xx-xx-xx-xx-xx",
  "powerState": "VM running",
  "privateIpAddress": "xx.x.x.x",
  "publicIpAddress": "xx.xxx.xx.xxx",
  "resourceGroup": "MyResourceGroup"
}
```

이제 새로 생성한 Windows Server VM 에 원격 데스크탑 및 (`az vm create` 출력으로 반환된) VM 공용 IP 주소를 사용하여 로그인합니다.
Windows 기반 시스템인 경우, `mstsc` 명령어를 사용하여 명령어 라인에서 실행할 수 있습니다:

```azurecli
mstsc /v:xx.xxx.xx.xxx
```

VM 생성에서 사용하였던 사용자 이름 / 암호 조합을 동일하게 제공하여 로그인을 합니다.

## Azure에서 다른 리소스 생성하기

지금까지 리소스 그룹, Linux VM, 그리고 Windows Server VM을 생성하는 방법을 살펴보았습니다. Azure 리소스 중 많은 다른 유형 또한 생성 가능합니다.

모든 새로운 리소스는 일관성있게 `az <resource type name> create` 이름 패턴을 사용하여 생성이 이루어집니다. 예를 들어, 새로 생성된 VM에 연결할 Azure 네트워크 로드 밸런서를 생성하기 위해서는 다음 생성 명령어를 사용 가능합니다:

```azurecli
az network lb create -n MyLoadBalancer -g MyResourceGroup
```

개인 가상 네트워크 (Azure 내에서는 일반적으로 "VNet" 으로 일컫음)를 다음 생성 명령어를 사용하여 인프라에 새로 생성할 수 있습니다:

```azurecli
az network vnet create -n MyVirtualNetwork -g MyResourceGroup --address-prefix 10.0.0.0/16
```

Azure 및 Azure CLI를 강력하게 만드는 요소는 클라우드 기반 인프라를 얻기 위해 사용할 수 있다는 것 뿐만 아니라
관리 플랫폼 서비스를 생성하기 위해 사용할 수 있다는 것입니다. 관리 플랫폼 서비스는 또한 인프라와 결합하여 보다 강력한 솔루션을 만들 수 있습니다.

예를 들어, Azure CLI를 사용하여 Azure AppService를 생성할 수 있습니다. Azure AppService는 인프라에 대한 걱정을 하지 않고 웹앱을 호스트하는 훌륭한 방법을 제공하는 관리 플랫폼 서비스입니다. Azure AppService를 생성한 다음에는, 다음 생성 명령어를 사용하여 AppService 내 두 개의 Azure Web App을 새로 생성할 수 있습니다:

```azurecli
# 내부에 임의의 개수에 대한 web app을 호스트 가능한 Azure AppService를 생성합니다
az appservice plan create -n MyAppServicePlan -g MyResourceGroup

# AppService 내 2개의 Web App을 생성합니다 (노트: name param은 유일한 DNS 항목이어야 합니다)
az appservice web create -n MyWebApp43432 -g MyResourceGroup --plan MyAppServicePlan 
az appservice web create -n MyWebApp43433 -g MyResourceGroup --plan MyAppServicePlan 
```

`az <resource type name> create` 패턴에 대한 기본을 이해한 다음에는, 임의의 리소스를 생성하는 것이 쉬워졌을 것입니다. 다음은
몇몇 대중적인 Azure 리소스 유형 및 각 유형을 생성하는데 대응하는 Azure CLI 생성 명령어입니다:

```
리소스 유형                 Azure CLI 생성 명령어
-------------               ------------------------
리소스 그룹                 az group create
가상 컴퓨터                 az vm create
가상 네트워크               az network vnet create
로드 밸린서                 az network lb create
관리 디스크                 az disk create
스토리지 계정               az storage account create
가상 컴퓨터 가용성 집합     az vmss create
Azure 컨테이너 서비스       az acs create
Web App                     az appservice web create
SQL 데이터베이스 서버       az sql server create
Document DB                 az documentdb create
```

[Reference documentation](/azure/doc-ref-autogen) 에 방문하여 각 선행되는 명령어와 생성하고자 하는 리소스 유형에 전달 가능한 부가적인 리소스에 특화된 매개변수에 대해 보다 자세히 학습합니다.

## 유용한 팁: --no-wait를 사용한 생성 동작 최적화

디폴트로 Azure CLI 2.0을 사용하여 리소스를 생성할 때, `az <resource type name> create` 명령어는 해당 리소스가 생성되어
사용 준비가 되었을 때까지 기다립니다. 예를 들어, VM을 생성하는 경우, `az vm create` 명령어는 디폴트로 해당 VM이 생성되고
SSH 또는 RDP를 통해 접속 가능 준비가 될 때까지 반환되는 값이 없을 것입니다.

우리는 서로 의존성 (및 계속 진행하기 전 성공적으로 완료해야 하는 필요한 이전 단계)가 있는 여러 단계를 포함하는 자동화 스크립트를 작성하기 쉽게 해 주기 때문에 해당 접근 방식을 사용합니다.

계속 진행하기 전에 리소스 생성을 기다릴 필요가 없는 경우에는, `no-wait` 옵션을 사용하여 백그라운드에서 생성 단계를
시작할 수 있습니다. 다른 명령어를 위해 CLI 사용이 계속 가능합니다.

예를 들어, `az vm create` 에 대한 다음 사용 예는 VM 배포를 시작한 다음에 결과값을 보다 매우 빠르게 (그리고 VM 이 완전히 부팅되기 이전에)
반환합니다:

```azurecli
az vm create -n MyLinuxVM2 -g MyResourceGroup --image UbuntuLTS --no-wait
```

`--no-wait` 접근 방식을 사용하면 자동화 스크립트에 대한 성능을 대폭 최적화할 수 있도록 도와줍니다.

## 리소스 목록 보기 및 결과 포맷

Azure CLI 내에서 `list` 명령어를 사용하여 Azure에서 실행하는 리소스를 찾아 목록을 살펴볼 수 있습니다.

생성 명령어처럼, 모든 리소스 유형에 걸쳐 공통적으로 일관된 `az <resource type name> list` 이름 패턴 및 Azure CLI 2.0을 사용하여 리소스 목록을 볼 수 있습니다. 보고자 하는 선호 방식에 따라 리소스 목록 결과를 필터링 및 정렬 가능한 출력 포맷 및 쿼리 옵션이 있습니다.

예를 들어, `az vm list` 는 가지고 있는 모든 VM 목록을 보여줍니다.

```azurecli
az vm list 
```
반환되는 값은 디폴트로 JSON 입니다 (간단히 여기서는 출력 일부분만을 표시합니다).

```json
[
  {
    "availabilitySet": null,
    "diagnosticsProfile": null,
    "hardwareProfile": {
      "vmSize": "Standard_DS1_v2"
    },
    "id": "/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/DEMORG1/providers/Microsoft.Compute/virtualMachines/DemoVM010",
    "instanceView": null,
    "licenseType": null,
    "location": "westus2",
    "name": "MyLinuxVM",
    "networkProfile": {
      "networkInterfaces": [
        {
          "id": "/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/demorg1/providers/Microsoft.Network/networkInterfaces/DemoVM010VMNic",
          "primary": null,
          "resourceGroup": "MyResourceGroup"
        }
      ]
    },
          ...
          ...
          ...   
]
```

옵션으로 출력 포맷을 `--output` 옵션을 사용하여 변경할 수 있습니다. `az vm list` 명령어를 실행하여 이전에 생성한 Linux 및 Windows Server VM을 VM에 대한 가장 일반적인 속성과 함께 *table* 포맷 옵션으로 쉽게 읽을수 있도록 살펴봅니다.

```azurecli
az vm list --output table
```

```Output
Name       ResourceGroup    Location
---------  ---------------  ----------
MyLinuxVM  MyResourceGroup  westus2
MyWinVM    MyResourceGroup  westus2
```

*tsv* 출력 옵션은 임의의 헤더가 없는 텍스트 기반 및 탭으로 구분된 포맷을 얻기 위해 사용 가능합니다. 해당 포맷은 출력을
grep와 같은 다른 텍스트 기반 도구에 파이프하고자 할 때 유용합니다.

```azurecli
az vm list --output tsv
```

```
None    None            /subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyLinuxVM        None    None    westus2 MyLinuxVM                   None        Succeeded       MyResourceGroup None                    Microsoft.Compute/virtualMachines       XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
None    None            /subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWinVM  None    None    westus2 MyWinVM                 None    Succeeded       MyResourceGroup None                    Microsoft.Compute/virtualMachines       XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
```
리소스 목록 및 출력 포맷에 대한 부가적인 방법에 대해 알고 싶다면 [output formats](format-output-azure-cli.md) 게시물을 살펴봅니다.

## Querying resources and shaping outputs

Often you want to be able to query for only those resources that meet a specific condition.  

The `list` command has built-in support
that makes it easy to filter resources by Resource Group name.  For example, you can pass either a `--ResourceGroup` or `-g` parameter
to a `list` command to only retrieve those resources within a specific resource group:

```azurecli
az vm list -g MyResouceGroup --output table
```

```Output
Name       ResourceGroup    Location
---------  ---------------  ----------
MyLinuxVM  MyResourceGroup  westus2
MyWinVM    MyResourceGroup  westus2
```

For even more powerful querying support, you can use the `--query` parameter to execute 
a JMESPath query on the results of *any* `az` command.  JMESPath queries can be used both to filter as well
as shape the output of any returned result.

For example, execute the following command to query for any VM resource within any resource group that contains the letters "My":

```azurecli
az vm list --output table --query "[?contains(resourceGroup,'MY')]" 
```

```Output
ResourceGroup    ProvisioningState    Name       Location    VmId
---------------  -------------------  ---------  ----------  ------------------------------------
MYRESOURCEGROUP  Succeeded            MyLinuxVM  westus2     XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
MYRESOURCEGROUP  Succeeded            MyWinVM    westus2     XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX
```

We could then choose to further refine the output by using the shaping capability of JMESPath queries to output different values
as well.  For example, the following command retrieves the type of OS disk the VM is using to determine whether the OS is Linux or Windows based:

```azurecli
az vm list --output table --query "[?contains(resourceGroup,'MY')].{ VMName:name,OSType:storageProfile.osDisk.osType }" 
```

```Output
VMName     OSType
---------  --------
MyLinuxVM  Linux
MyWinVM    Windows
```

The JMESPath support in Azure CLI is powerful.  Learn more about how to use it in our [query](query-azure-cli.md) article.

## Deleting resources

You can use the `delete` command within Azure CLI to delete the resources you no longer need. You can use the `delete` command with 
any resource just like you can with the `create` command.

```azurecli
az vm delete -n MyLinuxVM -g MyResourceGroup
```

By default the CLI prompts to confirm deletion.  You can suppress this prompt for automated scripts.

```Output
Are you sure you want to perform this operation? (y/n): y
EndTime                           Name                                  StartTime                         Status
--------------------------------  ------------------------------------  --------------------------------  ---------
2017-02-19T02:35:56.678905+00:00  5b74ab80-9b29-4329-b483-52b406583e2f  2017-02-19T02:33:35.372769+00:00  Succeeded
```

You can also use the `delete` command to delete many resources at a time. For example, the following command deletes all the 
resources in the "MyResourceGroup" resource group that we've used for all the samples in this Get Started tutorial.

```azurecli
az group delete -n MyResourceGroup
```

```Output
Are you sure you want to perform this operation? (y/n): y
```

## Get samples

To learn more about ways to use the Azure CLI, check out our most common scripts for
[Linux VMs](/azure/virtual-machines/virtual-machines-linux-cli-samples?toc=%2fcli%2fazure%2ftoc.json&bc=%2fcli%2fazure%2fbreadcrumb%2ftoc.json),
[Windows VMs](/azure/virtual-machines/virtual-machines-windows-cli-samples?toc=%2fcli%2fazure%2ftoc.json&bc=%2fcli%2fazure%2fbreadcrumb%2ftoc.json), 
[Web apps](/azure/app-service-web/app-service-cli-samples?toc=%2fcli%2fazure%2ftoc.json&bc=%2fcli%2fazure%2fbreadcrumb%2ftoc.json),
and [SQL Database](/azure/sql-database/sql-database-cli-samples?toc=%2fcli%2fazure%2ftoc.json&bc=%2fcli%2fazure%2fbreadcrumb%2ftoc.json).

## Read the API reference docs

[API reference](/cli/azure)

## Get help

The Azure CLI has built-in help documentation, which matches our web documentation that you can run from the command line:

```azurecli
az [command-group [command]] -h
```

For example, to see what commands and subgroups are available for VMs, use:

```azurecli
az vm -h
```

To get help with the command to create a VM, use:

```azurecli
az vm create -h
```

## Switch from Azure CLI 1.0

If you already know how to use Azure CLI 1.0 (azure.js),
you'll notice places where the commands aren't quite the same.
Sometimes the commands to perform a task are significantly different.
To help you make the switch from Azure CLI 1.0 to Azure CLI 2.0,
we've started this [command mapping](https://github.com/Azure/azure-cli/blob/master/doc/azure2az_commands.rst).

## Send us your feedback

```azurecli
az feedback
```
