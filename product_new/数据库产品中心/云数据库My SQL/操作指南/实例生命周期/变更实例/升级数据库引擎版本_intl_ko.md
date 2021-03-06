## 작업 시나리오
이 파일은 TencentDB for MySQL 엔진 에디션을 업그레이드할 때 콘솔에서 에디션을 업그레이드하는 방법을 소개하였습니다.
TencentDB for MySQL는 다음 에디션의 데이터베이스 엔진 업그레이드를 지원합니다.
- MySQL 5.5로부터 MySQL 5.6
- MySQL 5.6로부터 MySQL 5.7

<span id="shengjiguize"></span>
## 에디션 업그레이드 규범
- 메인 에디션을 크로스하여 업그레이드할 수 없습니다. 예를 들면 TencentDB for MySQL 5.5 데이터베이스 인스턴스를 MySQL 5.7 혹은 이상 에디션으로 업그레이드할 수 없습니다. 데이터베이스 인스턴스를 반드시 MySQL 5.6 에디션으로 업그레이드해야 합니다.
- `create table …  as select …` 문법을 지원하지 않습니다.
- TencentDB for MySQL 5.6/5.7 마스터-슬레이브 동기화는 GTID를 기반으로 구현하며, 기본적으로 InnoDB 엔진만 지원합니다.
- MySQL 5.5 에디션을 MySQL 5.6 에디션으로 업데이트 시 MyISAM 엔진의 테이블을 InnoDB로 변경합니다. **업데이트 전에 MyISAM을 InnoDB로 교체해주시기 바랍니다.
- 업데이트 기간에 TencentDB for MySQL는 slow\_log 테이블을 삭제합니다. 혹 로그 메시지를 보류하려면 메인 에디션으로 업그레이드하기 전에 로그 내용을 저장해주시기 바랍니다.
- **에디션을 업데이트하려는 인스턴스에 기타 인스턴스(마스터 인스턴스, 읽기 전용 인스턴스 등)를 연동하였을 경우, 복제된 데이터의 일치성을 위해 동기로 에디션을 업데이트합니다**.
- TencentDB for MySQL 에디션 업그레이드 시, 데이터를 마이그레이션해야 합니다. 오랜 시간이 소모되므로, 잠시만 기다려주시기 바랍니다. 마이그레이션 작업은 서비스에 영향을 미치지 않으며, 액세스 가능합니다.
- 에디션 업그레이드를 완료하면 인스턴스를 변경(초급 단위로 MySQL 데이터베이스 연결이 끊깁니다)해야 합니다. 프로그램에 자동 재연결 기능이 적용되어있으므로 인스턴스를 점검하는 시간에 변경하시기 바랍니다. 점검 시간은 [인스턴스 점검시간 설정](https://cloud.tencent.com/document/product/236/10929)을 참조하십시오.
- 낱개 인스턴스의 테이블 수량은 100만을 초과 시에 업그레이드에 실패할 수 있습니다. 또한 데이터베이스 모니터링에도 영향을 미칠 수 있으므로, 테이블 수량을 합리적으로 기획하고 낱개 인스턴스 테이블 수량은 100만 미만으로 제어하시기 바랍니다.

## 조작 프로세스
1. [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb/)에 로그인합니다..
2. 인스턴스 리스트에서 업그레이드하려는 인스턴스를 선택하고, 조작 칼럼에서 [더 알아보기]>[에디션 업그레이드]를 선택합니다(MySQL 5. 7은 더 높은 에디션으로 업그레이드할 수 없습니다).
![](https://main.qcloudimg.com/raw/ec14ff513f80db6e87338b5a531f6126.png)
3. 팝업창에서 원하는 데이터베이스 에디션을 선택하고 [업그레이드]를 클릭합니다.
데이터베이스 에디션을 업그레이드 시에 데이터 마이그레이션과 연관되므로, 업그레이드를 완료하면 초급 단위로 MySQL 인터페이스 연결이 플래시합니다. 업그레이드를 시작할 때 [점검시간내]로 변경하면 인스턴스 업그레이드를 완료한 후에 [점검시간]내에 변경할 수 있습니다.
> [점검시간내]로 시간을 변경할 경우 데이터베이스 스펙을 업그레이드 시 바로 변경하는것이 아닙니다. 인스턴스의 [점검시간] 변경 요청을 받을 때까지 동기화하므로 전체 인스턴스를 업그레이드하는 시간이 길어질 수 있습니다.
>
![](https://main.qcloudimg.com/raw/8a27b736891296d8c64077cf01409f08.png)

