### 인스턴스에 로그인하기 전에 어떤 포트를 개방해야 하나요?
일반적으로 Linux 인스턴스는 22번 포트를 개방해야 하고, Windows 인스턴스는 3389번 포트를 개방해야 합니다. 그 외 다른 인스턴스 유형에 적용할 수 있는 포트는 [보안 그룹 응용 사례](https://intl.cloud.tencent.com/document/product/213/32369)를 참조 바랍니다.

### CVM에서 흔히 사용하는 포트는 어떤 것들이 있나요?

[서버 상용 포트](https://intl.cloud.tencent.com/document/product/213/12451)를 참조 바랍니다.

### 왜 포트를 열어야 하며, 특정 포트를 열려면 어떻게 해야 하나요?

보안 그룹에서 포트를 개방해야 포트에 해당하는 서비스를 사용할 수 있습니다. 예:
8080 포트를 사용하여 웹 페이지에 액세스하고자 한다면 보안 그룹에서 해당 포트를 활성화하고 해당 포트를 개방한 상태에서만 액세스할 수 있습니다.
포트를 개방하는 작업 순서는 아래와 같습니다.
1. [보안 그룹 콘솔](https://console.cloud.tencent.com/vpc/securitygroup)에 로그인하고, 해당 인스턴스에 바인딩된 보안 그룹을 클릭하여 상세 페이지로 이동합니다.
2. 인바운드 규칙/아웃바운드 규칙을 선택하여, 규칙 추가를 클릭합니다.
3. 사용자의 IP 주소(세그먼트) 및 개방이 필요한 포트 정보를 입력하여 개방 허용을 선택합니다.
자세한 작업 순서는 [보안 그룹 규칙 추가](https://intl.cloud.tencent.com/document/product/213/34272)를 참조 바랍니다.

### CVM 원격 기본 포트는 어떻게 수정하나요?

자세한 작업 방식은 [CVM 원격 기본 포트 수정](https://intl.cloud.tencent.com/document/product/213/35376)을 참조 바랍니다.


### 포트를 수정한 후 서비스를 사용할 수 없는 이유는 무엇인가요?

서비스 포트를 수정한 후에는, 해당하는 보안 그룹에서도 해당 포트를 개방해야 합니다. 그렇지 않으면 서비스를 사용할 수 없습니다.

### Tencent Cloud가 지원하는 포트는 어떤 게 있나요?

- Tencent Cloud는 기본적으로 TCP:25 포트를 차단합니다. 해당 제한을 취소해야 한다면 [25 포트 차단 해제](https://intl.cloud.tencent.com/document/product/213/34833)를 참조하여 차단 해제를 신청할 수 있습니다.
- 일부 포트에는 보안 위험성이 있어 Tencent Cloud에서 제한하지 않아도 통신사에서 차단하기 때문에 액세스할 수 없습니다. 이런 상황에 대비하여 포트를 변경해야 하며, 다음과 같은 포트를 사용해 리슨하지 말 것을 권장합니다.
<table>
<tr><th>프로토콜</th><th>차단 가능한 포트</th></tr>
<tr><td>TCP</td><td>42, 135, 137, 138, 139, 445, 593, 1025, 1434, 1068, 3127, 3128, 3129, 3130, 4444, 5554, 5800, 5900, 9996</td></tr>
<tr><td>UDP</td><td>1026, 1027, 1434, 1068, 5554, 9996, 1028, 1433, 135 - 139</td></tr>
</table>


### TCP 25 포트에 액세스할 수 없는 이유는 무엇인가요?
TCP 25 포트는 기본 설정된 이메일 서비스 포트입니다. 보안상의 이유로 CVM 인스턴스의 25 포트는 차단 상태로 기본 설정되어 있습니다. TCP 25 포트를 사용해야 한다면 차단 해제를 신청하시기 바라며, 자세한 작업 방식은 [25 포트 차단 해제](https://intl.cloud.tencent.com/document/product/213/34833)를 참조 바랍니다.

