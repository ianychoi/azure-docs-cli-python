---
title: Install the Azure CLI 2.0
description: Reference docs for Azure CLI 2.0
keywords: Azure CLI 2.0, Azure CLI 2.0 Reference, Install Azure CLI 2.0, Azure Python CLI, Uninstall Azure CLI 2.0
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/06/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: azurecli
ms.service: multiple
ms.assetid: ea5c0ee1-c530-4a1e-a83f-e1be71f6d416
---

# Azure CLI 2.0 설치

새로운 버전의 Azure CLI를 지금 설치해 봅시다!
Azure 자원을 관리하기 위해 훌륭한 native 명령어 라인 경험을 제공하기 위해 개선 및 업데이트를 하였습니다.
macOS, Linux, 그리고 Windows에서 사용 가능합니다.
최신 릴리즈에 대한 자세한 정보는 [릴리즈 노트](release-notes-azure-cli.md) 를 살펴봅니다.

> [!NOTE]
> 이전 버전의 Azure CLI를 필요로 하는 경우에는 [Azure 1.0 설치](/azure/cli-install-nodejs) 방법을 살펴봅니다.

## macOS

1. Azure CLI 2.0를 `curl` 명령어로 설치합니다.

   ```bash
   curl -L https://aka.ms/InstallAzureCli | bash
   ```

2. 명령어 쉘에 대한 몇몇 변경 사항을 적용하기 위해 재시작해야 할 것입니다.

   ```bash
   exec -l $SHELL
   ```
   
3. 명령 프롬프트에서 `az` 명령어를 사용하여 Azure CLI 2.0를 실행합니다.

> [!Note]
> 제거하려면 [수동 제거 방법](#uninstall)을 살펴봅니다.

## Windows

Windows에서는 `pip` 를 사용하여 Azure CLI 2.0을 가져옵니다.

1. Python 사이트에 방문하여 Windows용 [Python 다운로드](https://www.python.org/downloads/) 를 수행합니다.
   Python을 설치할 때 Pip 구성요소를 설치하는지를 확인합니다.
   설치를 완료한 후에는, Python을 PATH 환경변수 (설치 관리자에서 나타날 것입니다)에 Python을 추가합니다.

2. Python 설치를 명령 프롬프트에서 확인합니다.

   ```bash
   python --version
   ```

3. `pip` 를 사용하여 Azure CLI 2.0을 설치합니다.

   ```bash
   pip install --user azure-cli
   ```

   > [!NOTE]
   > CLI `az.bat` 는 `%USERPROFILE%\AppData\Roaming\Python\Scripts` 위치 또는
   > `%USERPROFILE%\AppData\Roaming\Python\PythonXY\Scripts` 위치이며,
   > `XY` 는 사용하는 Python 버전 (예를 들면, `%USERPROFILE%\AppData\Roaming\Python\Python27\Scripts`) 에 위치할 것입니다.
   > `az.bat` 를 포함하는 폴더를 경로에 추가합니다.
   
4. 명령 프롬프트에서 `az` 명령어를 사용하여 Azure CLI 2.0를 실행합니다.

## Linux

1. Linux에서는 특정 [필수 사항](#linux-prerequisites) 을 설치해야 할 수도 있습니다.

2. Azure CLI 2.0를 `curl` 명령어로 설치합니다.

   ```bash
   curl -L https://aka.ms/InstallAzureCli | bash
   ```

3. 명령어 쉘에 대한 몇몇 변경 사항을 적용하기 위해 재시작해야 할 것입니다.

   ```bash
   exec -l $SHELL
   ```

4. 명령 프롬프트에서 `az` 명령어를 사용하여 Azure CLI 2.0를 실행합니다.

> [!Note]
> 제거하려면 [수동 제거 방법](#uninstall)을 살펴봅니다.

## Docker

Azure CLI를 사전 구성한 Docker 이미지를 관리하고 있습니다.

Azure CLI를 `docker run` 명령어를 사용하여 설치합니다.

```bash
docker run azuresdk/azure-cli-python:<version>
```

사용 가능한 버전에 대한 [Docker tags](https://hub.docker.com/r/azuresdk/azure-cli-python/tags/) 를 살펴봅니다.

> [!NOTE]
> 사용자 환경에 대한 SSH 키를 선택하고자 하는 경우,
> `-v ${HOME}:/root` 를 사용하여 $HOME을 `/root` 로 마운트 가능합니다.
>
> ```bash
> docker run -v ${HOME}:/root azuresdk/azure-cli-python:<version>
> ```

Docker 이미지는 [`component` 기능](/cli/azure/component) 을 지원하지 않습니다.
Azure CLI 2.0을 업데이트하려면, `docker run` 을 사용하여 최신 이미지 또는 원하는 특정 이미지를 설치합니다.

## apt-get

Debian/Ubuntu 기반 시스템에서는 `apt-get` 을 통해 Azure CLI 2.0을 설치할 수 있습니다.

1. 소스 리스트를 수정합니다.

   - 32비트 시스템

     ```bash
     echo "deb https://packages.microsoft.com/repos/azure-cli/ wheezy main" | \
          sudo tee /etc/apt/sources.list.d/azure-cli.list
     ```

   - 64비트 시스템

     ```bash
     echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ wheezy main" | \
          sudo tee /etc/apt/sources.list.d/azure-cli.list
     ```

2. 다음 sudo 명령어를 실행합니다:

   ```bash
   sudo apt-key adv --keyserver packages.microsoft.com --recv-keys 417A0893
   sudo apt-get install apt-transport-https
   sudo apt-get update && sudo apt-get install azure-cli
   ```

apt-get을 통해 설치하는 경우, `az component` 를 지원하지 않습니다.
CLI를 업데이트하려면, 다음 명령어를 사용합니다:

```bash
sudo apt-get update && sudo apt-get install azure-cli
```

## Linux Prerequisites

1. [Python](https://www.python.org/downloads) 이 없다면, 설치합니다.

2. Linux 배포판에 따라, 필수 사항을 설치합니다.

   ```
   플랫폼                | 필수 사항
   ----------------------|---------------------------------------------
   Ubuntu 15.10 or 16.04 | sudo apt-get update && sudo apt-get install -y libssl-dev libffi-dev python-dev build-essential
   Ubuntu 12.04 or 14.04 | sudo apt-get update && sudo apt-get install -y libssl-dev libffi-dev python-dev
   Debian 8              | sudo apt-get update && sudo apt-get install -y libssl-dev libffi-dev python-dev build-essential
   Debian 7              | sudo apt-get update && sudo apt-get install -y libssl-dev libffi-dev python-dev
   CentOS 7.1 or 7.2     | sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel
   RedHat 7.2            | sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel
   SUSE OpenSUSE 13.2    | sudo zypper refresh && sudo zypper --non-interactive install gcc libffi-devel python-devel openssl-devel
   ```

## 문제 해결
-------------------------------

### curl 리디렉션 오류

`-L` 매개변수에 관한 `curl` 명령어 오류, 또는 "Object Moved" 를 설명하는 오류를 반환한 경우, aka.ms 주소 대신 full url을 사용해 봅니다:

```
# 다음 (메시지가) 보이는 경우:
curl -L https://aka.ms/InstallAzureCli | bash
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   175  100   175    0     0    562      0 --:--:-- --:--:-- --:--:--   560
bash: line 1: syntax error near unexpected token `<'
'ash: line 1: `<html><head><title>Object moved</title></head><body>

#### 대신 아래와 같이 시도합니다:
curl https://azurecliprod.blob.core.windows.net/install | bash
```


### `cffi` 또는 암호와 관련된 설치 오류

OS X 설치에서 오류를 발견하는 경우에는 `pip` 를 업그레이드합니다.

```bash
pip install --upgrade --force-reinstall pip
```

**Debian** 또는 **Ubuntu** 설치에서 오류를 발견한 경우에는 해당 예제와 같이 `libssl-dev` 및 `libffi-dev` 를 설치합니다.

```bash
sudo apt-get update
sudo apt-get install -y libssl-dev libffi-dev
```

또한 Python 대상 버전에 따는 Python 개발 (관련 라이브러리)를 설치합니다.

Python 2:

```bash
sudo apt-get install -y python-dev
```

Python 3:

```bash
sudo apt-get install -y python3-dev
```

Ubuntu 15 는 `build-essential` 또한 필요로 할 수도 있습니다:

```bash
sudo apt-get install -y build-essential
```

### 오류 예시

```
Downloading cffi-1.5.2.tar.gz (388kB)
    100% |################################| 389kB 3.9MB/s
    Complete output from command python setup.py egg_info:

        No working compiler found, or bogus compiler options
        passed to the compiler from Python's distutils module.
        See the error messages above.
        (If they are about -mno-fused-madd and you are on OS/X 10.8,
        see http://stackoverflow.com/questions/22313407/ .)

    ----------------------------------------
Command "python setup.py egg_info" failed with error code 1 in /tmp/pip-build-77i2fido/cffi/
```

```
#include <openssl/e_os2.h>
                            ^
compilation terminated.
error: command 'x86_64-linux-gnu-gcc' failed with exit status 1

Failed building wheel for cryptography
```

Stack Overflow 질문을 살펴봅니다 - [PIP 및 setup.py를 통한 Python Cryptography 패키지 설치 실패](http://stackoverflow.com/questions/22073516/failed-to-install-python-cryptography-package-with-pip-and-setup-py)

## 설치 제거

https://aka.ms/InstallAzureCli 스크립트를 사용하여 CLI를 설치한 경우, 다음 단계를 통해 설치 제거가 가능합니다.

1. 설치한 파일을 삭제합니다.

   ```bash
   rm -r <install location>/lib/azure-cli
   rm <install location>/bin/az
   ```

2. <install location>/.bash_profile 에서 `<install location>/lib/azure-cli/az.completion` 줄을 삭제합니다.

> [!Note]
> 디폴트 설치 경로는 /Users/<username> 입니다.

pip, apt-get, 또는 Docker를 사용하여 설치한 경우, 동일한 도구를 사용하여 설치를 제거합니다.

## 이슈 보고 및 피드백

해당 도구를 사용하면서 버그 상황을 접한 경우에는,
이슈를 GitHub 저장소 내 [Issues](https://github.com/Azure/azure-cli/issues) 에 보고합니다.
명령어 라인에 대한 피드백을 작성하려면, `az feedback` 명령어를 사용합니다.
