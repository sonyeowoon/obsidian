su를 제한하는 이유
sudo를 사용하기 위해서는 sudo그룹에 속한 유저들만 사용할 수 있어야 한다.
super user 권한을 만약 모두가 sudo명령을 사용할 수 있는 권한을 가지게 된다면 이는 보안 문제로 직결된다.
과제상에서는 sudo그룹 추가로 아무나 sudo로 접근하지 못할 것을 해 놓았지만, su를 통해 다른 유저들도 root에 접근할 수 있는 여지가 있다.
이를 방지하고자 sudo그룹에 속한 유저들은 root권한을 사용할 수 있는 유저이니, sudo그룹이 아닌 사용자들은 su를 사용하지 못하게 할 것이다.
# su파일 편집하기
하단의 /etc/pam.d디렉토리로 이동한다.
![[Pasted image 20240426155558.png]]
`vim su`를 통해 su파일을 편집할 것이다.

![[Pasted image 20240426160147.png]]
편집에 들어가서
```
auth required pam_wheel.so use_uid group=sudo
```
구문을 추가해준다.
해당 구문은 `sudo`라는 그룹에 su명령을 사용할 수 있도록 한다.
만약 `group=su`를 명시하지 않으면 기본적으로 wheel 그룹을 대상으로 한다.
![[Pasted image 20240426162131.png]]
hoyhoy user는 지금 그룹이 없다.(자기자신)
때문에 su를 시도하면.. permission denied라고 뜬다.