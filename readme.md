# 시작하기

이 가이드는 첫 번째 Kubernetes 클러스터를 만들고 Windows 웹 서버를 배포하는 데 필요한 모든 단계를 안내합니다. 다음 단계가 포함됩니다.

- 올바른 도구 얻기
- 배포하려는 내용을 설명하는 AKS 엔진 API 모델 완성
- Azure Resource Manager 템플릿 (이하 ARM 템플릿) 생성을 위한 AKS 엔진 실행
- Windows Server 19H1 노드에서 첫 번째 Kubernetes 클러스터 배포
- Windows 시스템에서 클러스터 관리
- 클러스터에 첫 번째 앱 배포

이 모든 단계는 모든 OS 플랫폼에서 수행 할 수 있으므로 일부 섹션은 Windows, Mac 또는 Linux에서 분리되어 가장 관련성 높은 샘플 및 스크립트를 제공합니다. 만약 Windows OS 환경에서 리눅스 버전의 도구를 사용하고 싶다면, [Linux용 Windows 서브 시스템](https://docs.microsoft.com/en-us/windows/wsl/about)을 설정하면 이 페이지의 Linux 지시 사항을 따를 수 있습니다.

이 핸즈온랩 모듈을 완료하면 Linux와 Windows Server 19H1 워커 노드를 포함하는 Kubernetes v1.15 버전의 Kubernetes 클러스터를 완성하여 사용할 수 있습니다.

# 모듈 구성

이 핸즈온랩 모듈은 다음의 단원으로 구성되어있습니다.

- [Chapter 1 - 필요한 소프트웨어 및 구성 요소 준비](chapter1.md)
- [Chapter 2 - AKS Engine API 모델 만들고 배포하기](chapter2.md)
- [Chapter 3 - 첫 애플리케이션 배포하기](chapter3.md)
