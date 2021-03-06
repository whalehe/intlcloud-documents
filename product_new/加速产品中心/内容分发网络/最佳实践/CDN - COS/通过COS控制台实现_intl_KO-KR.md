본 문서는 COS 콘솔에서 CDN이 COS을 가속하는 전체적인 작업 절차 및 방법을 설명해줍니다.

## 전제조건
1. Tencent Cloud 계정 가입 및 실명 인증을 완료하십시오.
2. CDN 서비스를 활성화하십시오. 자세한 내용은 [CDN 시작하기](https://intl.cloud.tencent.com/document/product/228/32978)를 참조하십시오.

## 운영 가이드

###버킷 생성하기
버킷 생성을 생성하십시오. 자세한 내용은 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309)을 참조하십시오.

## 가속 서비스 설정
1. 버킷을 생성한 후 해당 버킷의 설정 관리 페이지로 이동하거나 버킷 리스트에서 설정이 필요한 버킷의 작업 메뉴의 [관리 설정]을 클릭합니다. 설정 관리 페이지로 이동하고 [도메인 이름]을 선택하십시오.
2.**기본 가속 도메인 이름**을 사용하도록 설정하십시오.
**기본 가속 도메인 이름**은 시스템에서 기본으로 생성된 것으로 CDN 가속 노드를 통과하는 도메인 이름이며 사용자가 시작이나 닫기를 선택할 수 있습니다.
(1) 기본 가속 도메인 모듈에서 [편집]을 클릭하여 수동으로 현 상태를 시작하며 기본 가속 설정으로 이동하십시오.
![](https://main.qcloudimg.com/raw/260fde070f4b2f999c0d9d09bec13d55.png)
(2) 기본 가속 설정：
![](https://main.qcloudimg.com/raw/2b72c25d2bf11f0c53a2e8286fcecf07.png)
**원본 서버 유형** :일반적으로 **기본 원본 서버**이지만 원본 서버 버킷에 대해 정적 웹 사이트를 사용하도록 설정하고 해당 사이트를 가속하려면 **정적 웹 사이트 원본 서버**를 선택하십시오.
**Origin-pull 인증**： 버킷이 공개 읽기일 경우 Origin-pull 인증을 활성활 필요가 없으며 개인 읽기일 경우 CDN 서비스 인증을 활성해야 하며 Origin-pull 인증을 수동으로 활성화해야 합니다. 더 많은 정보는[Origin-pull 인증](https://intl.cloud.tencent.com/document/product/436/31505)을 참조하십시오.
**CDN 서비스 인증**: [CDN 서비스 인증 추가]를 클릭하여 CDN이 버킷 리소스에 대한 액세스 동의를 선택하십시오.
![](https://main.qcloudimg.com/raw/41e745800445225d042ef82c6febcc19.png)
(3) 설정 완료 시 [저장]을 클릭하여 CDN 가속을 활성화하십시오.
![](https://main.qcloudimg.com/raw/5ffc31cb49410b4685316e75860c9385.png)

>개인 읽기 버킷의 경우 원본 서버 인증과 CDN 서비스 인증을 모두 사용 시 CDN을 통한 원본 서버 접속에는 서명이 필요하지 않으며 CDN 캐시 리소스가 공용 네크워크에 전송되어 데이터 보안에 영향을 미치게 됩니다. 따라서 CDN 인증을 사용하도록 권장합니다.
>
2.**사용자 지정 가속 도메인 이름**을 사용하도록 설정하십시오.
사용자가 버킷에 이미 파일링한 ** 사용자 지정 도메인 이름**을 연동시키고 CDN 가속을 사용하도록 설정할 수 있습니다.
> COS 콘솔에서 최대 사용자 지정 도메인 이름 10개를 추가할 수 있습니다.
>
(1) ** 사용자 지정 가속 도메인 이름 ** 모듈에서 [도메인 이름 추가]를 클릭하여 ICP비안이 된 사용자 지정 도메인 이름을 추가하십시오.
![](https://main.qcloudimg.com/raw/eda34cc24d82cebf109e3507a2ae142f.png)
(2) 도메인 이름 설정은 다음과 같습니니다.
**도메인 이름**: 연동할 사용자 지정 도메인 이름을 입력하십시오(예: www.example.com). 입력한 도메인 이름은 파일링되고 DNS 서비스 제공 업체에 대응되는  CNAME가 구성되어 있는지 확인하십시오. 자세한 내용은 [CNAME 구성](https://intl.cloud.tencent.com/document/product/228/3121)을 참조하십시오.
**Origin-pull 인증**：개인 읽기 버킷에 대해서 Origin-pull 인증을 수동으로 활성화함으로 원본 서버를 보호하십시오.
설정을 완료 시 [저장]을 클릭하여 도메인 이름을 즉시 추가할 수 있습니다.
![](https://main.qcloudimg.com/raw/e21189d91929209ded554581d267a505.png)
>개인 읽기 버킷의 경우 원본 서버 인증과 CDN 서비스 인증을 모두 사용 시 CDN을 통한 원본 서버 접속에는 서명이 필요하지 않으며 CDN 캐시 리소스가 공용 네크워크에 전송되어 데이터 보안에 영향을 미치게 됩니다. 따라서 CDN 인증을 사용하도록 권장합니다.
>
(3) 저장된 후 **CDN 인증**열에 CDN 인증 기능 스위치가 표시되며 사용자 지정 도메인 이름에 대해 CDN 인증을 수동으로 사용할 수 있습니다.
**CDN 인증：** 타임스탬프 인증 설정을 활성하면 사용자의 콘텐츠 도용을 방지할 수 있어 도메인 이름을 추가한 다음 설정하십시오.

COS 콘솔에서 CDN이 COS를 가속하는 더 많은 콘텐츠는 [COS 도메인 관리 개요](https://intl.cloud.tencent.com/document/product/436/18424)를 참조하십시오.
