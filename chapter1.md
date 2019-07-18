# Azure 구독 준비하기

[https://www.azure.com/](https://www.azure.com/) 에 접속하여 일정 기간 동안 무료로 사용할 수 있는 Azure 구독을 활성화합니다.

**주의** 구독 생성 시 Pay-as-you-go 모델을 사용하면 사용량만큼 비용 청구가 곧바로 발생합니다. 이전에 Azure 구독을 만들기 위하여 제출한 적이 없었던 메일 계정을 이용하여 새로운 계정을 만드는 것을 추천합니다.

핸즈온랩 모듈을 오프라인에서 진행하는 경우 강사의 별도 지시가 있을 경우 그 지시에 따라 구독을 만들거나, 미리 제공되는 구독을 대신 사용할 수 있으니 확인하기 바랍니다.

# 필요한 도구 설치하기

이 핸즈온랩 모듈을 완료하기 위해서는 아래의 도구가 반드시 필요합니다. 모두 Windows, Mac 및 Linux에서 사용할 수 있습니다.

- Azure 구독 - 이 핸즈온랩 모듈을 Azure 구독 위에서 실행되는 것을 전제로 합니다. 트라이얼 버전의 구독을 [https://www.azure.com/](https://www.azure.com/) 에서 신청할 수 있습니다.
- AKS 엔진 - Kubernetes 클러스터를 자동으로 배포하는 ARM 템플릿을 생성하는 데 사용됩니다.
- Azure CLI - Azure에 로그인하고 리소스 그룹을 만들고 AKS 엔진으로 생성한 ARM 템플릿을 배포하는 데 사용됩니다.
- Kubectl - Kubernetes 클러스터를 관리하는 데 사용되는 도구입니다.
- SSH - 클러스터를 구축할 때 SSH 공개 키가 필요합니다. 나중에 관리 또는 문제 해결을 해야하는 경우 클러스터를 실행하는 Linux VM에 연결하는 데 사용됩니다.

그리고 실습의 편의를 위하여 이 핸즈온랩 모듈은 모든 명령줄 예시를 PowerShell 문법을 사용하여 설명합니다. Windows에서는 내장된 PowerShell을 사용할 수 있으며, Linux와 macOS에서는 PowerShell 6.0 이상을 별도로 설치하여 사용할 수 있습니다. 또한 원하지 않으면 PowerShell 대신 Bash 셸 문법이나 다른 방법으로 이 문서에서 설명하는 내용을 따라할 수도 있습니다.

> 만약 Windows OS에서 이 핸즈온랩 모듈을 따라하는데 문제가 있을 경우, 별도의 리눅스 가상 컴퓨터를 만들거나 Windows Subsystem for Linux를 사용하여 진행하시는 것을 권장합니다.

여러분께서 사용하는 컴퓨터 환경에 따라 적절한 Chapter를 찾아 설치를 진행하도록 합니다.

## Windows

Windows에는 PowerShell 5.x 버전이 이미 내장되어있습니다. 실습을 위해서 사용하는 PowerShell은 이 버전으로도 충분하므로 별도 설치는 필요하지 않습니다.

필요한 소프트웨어의 쉬운 설치를 위하여 Chocolatey Package Manager를 설치하도록 합니다.

관리자 권한으로 PowerShell을 시작한 다음, 아래 명령을 입력합니다.

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

설치가 끝난 후에는 아래 명령을 입력하여 설치를 완료합니다.

```powershell
choco install azure-cli -y
choco install kubernetes-cli -y
```

그리고 `winver` 명령을 실행하여 나타나는 화면에서 Windows 10 OS의 버전이 1803 이상인지 확인하여 그보다 낮은 경우 OpenSSH를 추가로 설치해주어야 합니다. 1803 이상의 버전에는 SSH 클라이언트가 OS에 내장되어있어서 별도 설치가 필요하지 않습니다.

```powershell
choco install openssh -y
```

## macOS

Homebrew Package Manager 또는 다른 패키지 매니저를 이용하여 설치를 진행합니다.

- azure-cli
- kubernetes-cli
- powershell

예를 들어 Homebrew 패키지 매니저를 이용하면 다음과 같습니다.

```bash
brew install azure-cli
brew install kubernetes-cli
brew cask install powershell
```

그 외에 `ssh`, `curl` 유틸리티는 이미 내장되어 되어있습니다.

## Linux

우선 아래 소프트웨어를 여러분이 사용하는 배포판의 패키지 소프트웨어 관리자를 통해 설치를 진행합니다.

- curl
- openssh
- tar

예를 들어 apt 패키지 매니저를 이용하면 다음과 같습니다.

```bash
apt install -y curl openssh tar
```

이어서 사용하는 패키지 매니저의 종류에 따라 Azure CLI 패키지 리포지터리를 등록하고 설치를 진행합니다.

- [Debian, Ubuntu Linux 계열 또는 apt를 사용하는 경우](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-apt?view=azure-cli-latest)
- [RHEL, CentOS, Fedora, Oracle Linux 계열 또는 yum을 사용하는 경우](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-yum?view=azure-cli-latest)
- [SUSE Linux 계열 또는 zypper를 사용하는 경우](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-zypper?view=azure-cli-latest)
- [기타 리눅스 배포판의 경우](https://docs.microsoft.com/ko-kr/cli/azure/install-azure-cli-linux?view=azure-cli-latest)

이어서 PowerShell Core를 설치합니다. [https://docs.microsoft.com/ko-kr/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-6](https://docs.microsoft.com/ko-kr/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-6) 에 각 배포판의 종류 별로 상세한 설치법이 나와있으므로 해당 가이드를 따라 설치를 진행합니다.

마지막으로 Kubernetes CLI를 설치합니다.

```bash
curl -L https://dl.k8s.io/v1.13.1/kubernetes-client-linux-amd64.tar.gz | tar xvzf -

sudo cp kubernetes/client/bin/kubectl /usr/local/bin/
```

# aks-engine 설치하기

필요한 소프트웨어들을 설치한 후에는 `aks-engine`을 OS 환경에 맞게 설치하고 구성해야 합니다.

여러분께서 사용하는 컴퓨터 환경에 따라 적절한 Chapter를 찾아 설치를 진행하도록 합니다.

## Windows

앞에서 설치한 Chocolatey 패키지 매니저를 이용하여 쉽게 설치할 수 있습니다.

```powershell
choco install aks-engine -y
```

## macOS

[https://github.com/Azure/aks-engine/releases](https://github.com/Azure/aks-engine/releases) 페이지에서 최신 버전의 AKS Engine을 다운로드하여 설치하도록 합니다. 이 때 Asset 파일 중에 파일 이름이 `-darwin-amd64.zip` 으로 끝나는 파일을 다운로드하여 사용합니다.

그 다음 해당 파일의 압축을 풀어 `aks-engine` 바이너리를 `/usr/local/bin` 디렉터리에 넣습니다.

## Linux

[https://github.com/Azure/aks-engine/releases](https://github.com/Azure/aks-engine/releases) 페이지에서 최신 버전의 AKS Engine을 다운로드하여 설치하도록 합니다. 이 때 Asset 파일 중에 파일 이름이 `-linux-amd64.zip` 으로 끝나는 파일을 다운로드하여 사용합니다.

그 다음 해당 파일의 압축을 풀어 `aks-engine` 바이너리를 `/usr/local/bin` 디렉터리에 넣습니다.

# AKS Engine 설치 검증

설치한 후에는 아래와 같이 AKS Engine이 정상적으로 실행되는지 확인합니다.

```
aks-engine version
Version: v0.38.1
...
```

# SSH 키 생성

새로 생성할 Kubernetes 클러스터에는 마스터 노드를 포함하여 1대 이상의 작업자 노드가 Linux를 사용합니다. 이 때 Linux 노드에 접속하기 위해서는 미리 SSH 공개 키를 만들어 지정해야 합니다.

PowerShell에서 아래 명령을 사용합니다.

```powershell
ls ~\.ssh\id_rsa.pub
```

만약 파일을 찾을 수 없다는 오류 메시지가 나타나면 `ssh-keygen` 명령을 실행하여 새 키를 만듭니다.

# Azure CLI 로그인

설치가 끝난 후 새 PowerShell 인스턴스를 시작하고, 다음 명령을 실행합니다.

```powershell
az login
``` 

그러면 웹 브라우저 창이 새로 나타납니다. 새로 만든 Azure 구독과 연결된 Microsoft Account로 로그인한 후, 창을 닫아도 좋다는 메시지가 나타나면 콘솔 창으로 되돌아갑니다.

잠시 기다리면 아래와 같은 메시지가 나타나면서 구독 정보들이 JSON 데이터로 표시됩니다.

```
You have logged in. Now let us find all the subscriptions to which you have access...

[
  {
    "cloudName": "AzureCloud",
    "id": "...",
    "isDefault": true,
    "name": "...",
    "state": "Enabled",
    "tenantId": "...",
    "user": {
      "name": "....",
      "type": "user"
    }
  }
]
```

여기까지 진행하였으면 [다음 Chapter](chapter2.md)로 이동합니다.
