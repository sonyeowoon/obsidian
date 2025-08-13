실수로 virtualbox에서 가상머신의 용량을 8GB로 주게되어 root의 용량을 모두 채워버렸다. 해결하는 과정을 정리해보려 한다.
***
# 가상머신의 용량 늘리기
VM VirtualBox의 `파일 - 도구 - 가상 미디어 관리자`로 진입해서 용량을 늘려줄 수 있다.
# logical volume늘리기
![[Pasted image 20240418003322.png]]
ldblk를 통해 sda 15기가로 여유공간이 생긴 것을 확인하였다.

![[Pasted image 20240418003425.png]]
```
sudo fdisk /dev/sda
```
이제 /dev/sda에 sda1파티션을 만들고 Linux LVM으로 바꿔줄 것이다.

![[Pasted image 20240418003605.png]]
n을 누르자 primart나 logical을 고를 수 있다.
![[Pasted image 20240418003755.png]]
p를 눌러 파티션을 고른다.
![[Pasted image 20240418003953.png]]
Partiton number에서 기본값으로 엔터.
First sector에서 기본값으로 엔터.
Last sector에서 +3G 입력 엔터.
![[Pasted image 20240418004107.png]]
sda3에 3GBdml 파티션을 만들어낸거 같다.
![[Pasted image 20240418004518.png]]
![[Pasted image 20240418004626.png]]
![[Pasted image 20240418004804.png]]
