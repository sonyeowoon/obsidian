응용프로그램이 있는 경우 공격자는 브루트 포스 시도를 사용하여 응용 프로그램에 액세스 할 수 있습니다.
Fail2ban은 악의적인 활동에 대한 서비스 로그를 모니터링하여 무차별 공격 및 기타 자동화된 공격으로부터 Linux 시스템을 보호하는 데 도움이 되는 도구입니다. 정규식을 사용하여 로그 파일을 검색합니다. 패턴과 일치하는 모든 항목이 계산되고 해당 항목이 미리 정의된 특정 임계값에 도달하면 Fail2ban은 특정 시간 동안 시스템 방화벽을 사용하는 위반 IP를 금지합니다. 금지 기간이 만료되면 IP 주소가 금지 목록에서 제거됩니다.
이 문서에서는 Debian 10에 Fail2ban을 설치하고 구성하는 방법을 설명합니다.
***
[참고글](https://mightyfriend.net/?p=3158)
# 설치 후 실행하기
아래 명령으로 설치합니다.
```
sudo apt install fail2ban
```
부팅 시 자동으로 시작되도록 시스템에 등록합니다.
```
sudo systemctl enable fail2ban
sudo systemctl restart fail2ban
```
# 설정파일 작성하기
fail2ban의 기본 설정은 `/etc/fail2ban/fail.conf`파일이다.
fail2ban 프로그램 업데이트할 때 설정이 덮어 쓰일 수 있다.
그래서 직접 수정하기 보다는 개인화 설정 파일인 `/etc/fail2ban/jail.local` 사용을 권장한다. jail.conf 설정을 보고 필요한 것을 가져와 jail.local을 만든다고 생각하면 쉬울 것 같다.
