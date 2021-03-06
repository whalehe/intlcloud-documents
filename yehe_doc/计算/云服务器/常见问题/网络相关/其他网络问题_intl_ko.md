### CVM에 로그인한 후 네트워크를 찾을 수 없습니다. 어떻게 해야 하나요?
CVM에 로그인한 후 웹 페이지에 액세스할 수 없는 등 네트워크를 찾을 수 없다면, DNS 설정 문제일 가능성이 있습니다. 다음의 작업을 참조하여 DNS를 자동 획득으로 설정하시기 바랍니다.
> 다음의 작업은 Windows Server 2012를 예시로 사용합니다.
> 
1. Windows CVM에 로그인합니다.
2. 운영 체제 인터페이스에서 <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;width: 22px;">를 클릭한 후, [제어판]>[네트워크 및 인터넷]>[네트워크 상태 및 작업 보기]>[어댑터 설정 변경]을 선택합니다.
3. [이더넷]을 우클릭한 후 [속성]을 선택하여 '이더넷 속성' 창을 엽니다.
4. '이더넷 속성' 창에서 [I인터넷 프로토콜 버전 4(TCP/IPv4)]를 더블클릭해 속성 창을 엽니다.
5. 아래 이미지와 같이, '인터넷 프로토콜 버전 4(TCP/IPv4) 속성' 창에서 [자동으로 IP 주소 받기]와 [자동으로 DNS 서버 주소 받기]를 선택하고 [확인]을 클릭합니다.
![](https://main.qcloudimg.com/raw/8a597efe05adc2f96d4b40b6cd633ca4.png)

### VPC 인스턴스와 기본 네트워크 인스턴스 간의 통신이 가능한가요?

#### 가능합니다. 단, 다음과 같은 제한이 있습니다.
VPC의 IP 대역 범위(CIDR)가 반드시 '10.0.0.0/16 ~ 10.0.47.0/16'(서브셋 포함)이어야 하며, 그렇지 않으면 충돌이 발생합니다.

#### 설정 순서:
[VPC 콘솔](https://console.cloud.tencent.com/vpc/vpc?rid=1)에 로그인한 후, VPC의 ID/이름을 클릭하여 VPC 상세 페이지로 이동합니다. **클래식링크**에서 통신하려는 기본 네트워크의 호스트를 연결하면 설정이 완료됩니다. 

### VPC와 통신되는 기본 네트워크 CVM은 어떻게 조회해야 하나요?
[VPC 콘솔](https://console.cloud.tencent.com/vpc/vpc?rid=1)에 로그인한 후, VPC의 ID/이름을 클릭하여 VPC 상세 페이지로 이동하면 **클래식링크**에서 해당 VPC의 CVM과 통신하는 기본 네트워크 CVM을 조회하실 수 있습니다.

### CVM을 중국 외 네트워크로 변경할 수 있나요?
CVM 구매 후에는 네트워크를 변경할 수 없으므로, 중국 외 네트워크가 필요할 경우 CVM을 반환하고 중국 외 서버를 재구매하시길 권장합니다.

### 내부 네트워크 DNS는 어떻게 설정하나요?
[내부 네트워크 DNS](https://intl.cloud.tencent.com/document/product/213/5225)를 참조 바랍니다.

### 동일한 IP 대역의 로컬 VPN에서 IP 대역의 IP를 획득할 수는 있지만, 인터넷에 접속할 수 없습니다. 어떻게 해야 하나요?

다음의 정보가 바르게 설정되었는지 확인하시기 바랍니다.
1. 수동으로 추가한 IP와 자동으로 획득한 IP가 동일한 IP의 서브넷에 있는지, 서브넷 마스크가 일치한지, 디폴트 게이트웨이가 설정되었는지, 디폴트 게이트웨이의 주소가 올바른지를 확인합니다.
2. DNS를 설정했는지, DNS 주소가 올바른지 확인합니다.
3. 위의 정보가 모두 바르게 설정되었다면, 정적 설정된 IP 주소에 IP 주소 충돌이 발생하지 않았는지 확인합니다.
  
위의 방법으로도 문제를 해결할 수 없을 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 문의 바랍니다.

### A 계정과 B 계정의 CVM을 동일한 내부 네트워크에 추가하려면 어떻게 해야 하나요?

계정 간 네트워크 통신 기능은 기본 제공되지 않습니다. 계정 간 네트워크 통신을 원하실 경우, [피어링 연결](https://intl.cloud.tencent.com/document/product/553/35190)이나 [CCN](https://intl.cloud.tencent.com/document/product/1003/31987) 서비스를 구매 바랍니다.
