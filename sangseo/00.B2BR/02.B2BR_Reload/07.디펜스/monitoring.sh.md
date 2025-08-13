# Architecture
```
uname -a
```
uname은 system 정보를 표시합니다.
--a 옵션은 man page 내에있는 옵션들을 순서대로 출력합니다.
***
# CPU physical
```
grep "physical id" /proc/cpuinfo
```
위 명령을 통해 물리cpu 몇개가 있는지 확인 가능하다.
`sort -u`(uniqe)를 통해서 겹치는 것들은 출력하지 않았다.
그리고 `wc -l`을 통해 몇개인지 출력해낼 수 있다.
***
# vCPU
```
grep -c processor /proc/cpuinfo
```
스레드 수를 카운팅 하여 가상 cpu 수를 구합니다.
## core와 thread
코어와 쓰레드에 대한 개념을 이해하려면 하이퍼스레딩 기능을 알아야 한다. 
> `하이퍼스레딩`
> 원래 한 개의 코어에서 일을 하는 동안 남는 잉여자원을 활용하는 기술이다. 코어를 효율적으로 사용하기 위한 기술이다.

한개의 코어는 1쓰레드로서 한가지 일만 할 수 있었지만, HT 기술을 통해 한개의 코어를 2개의 쓰레드로 나눔으로 두가지 작업을 동시에 할 수 있게 만든 기술이다.

HT 기술이 적용된 CPU는 한개의 코어가 2쓰레드로 동작하기 때문에 듀얼코어는 2코어 4쓰레드가 되는 것이고 쿼드코어는 4코어 8쓰레드가 되는 것이다. 

아래 두 CPU가 있다고 가정합니다.
+ HT 기술이 적용된 2코어 4쓰레드
+ 일반 4코어 4쓰레드
동클럭이라면 후자가 더 좋은 CPU라고 보면 됩니다.
***
### thread가 많으면 좋다?
#thread-safe #thread
어플리케이션의 실행이 무수히 많은 작업들로 쪼개져 CPU 코어 수보다 몇십배는 많은 스레드들이 생성되어 작업을 처리한다면 어떨까?

이러면 스레드들은 순서에 상관없이 마구잡이로 task를 처리한다.
결국 어플리케이션의 데이터는 서로 동기화되지 않고 1번 뷰, 2번 뷰에서 가져온 데이터는 서로 다른 데이터가 될 확률이 높다.

즉, thread-safe 하지 않게 된다.
만약 어플리케이션 동작이 순차적으로 실행되어야만 하는 특징이 있다면?
잘게 쪼개서 동시에 실행하기에 매우 어려운 성격의 어플리케이션이 있다면 실제로 사용할 수 있는 스레드 수는 한계가 있을 것이다.
***
# lscpu 명령
lscpu에서 
lscpu를 클러스터 pc에서 출력하면 아래와 같다. 
```
Architecture:            x86_64
  CPU op-mode(s):        32-bit, 64-bit
  Address sizes:         46 bits physical, 48 bits virtual
  Byte Order:            Little Endian
CPU(s):                  24
  On-line CPU(s) list:   0-23
Vendor ID:               GenuineIntel
  Model name:            13th Gen Intel(R) Core(TM) i7-13700
    CPU family:          6
    Model:               183
    Thread(s) per core:  2
    Core(s) per socket:  16
    Socket(s):           1
    Stepping:            1

```

![[Pasted image 20240416175116.png]]
모델명을 검색한 내용이다.
CPU(s)는 스레드 수를 나타낸다.
> `man lscpu`
> lscpu also displays the number of physical socket

Socket(s)는 피지컬 cpu를 나타낸다.
## 기타 명령어
```
cat /proc/cpuinfo | grep processor | wc -l
```
/proc/cpuinfo 를 통해서 보여지는 프로세서의 숫자는 프로세서의 실제 코어 갯수가 아닐수도 있습니다. 예를들어 2개의 코어를 가진 프로세서로 하이퍼쓰레딩(hyperthreading)을 한다면  4개의 코어로 표시가 될 수 있습니다.
코어의 실제 갯수를 구하기 위해서는 코어 아이디를 체크해야 합니다.
```
➜  ~ cat /proc/cpuinfo | grep 'core id'
core id		: 0 //1
core id		: 0 //2
core id		: 4 //3
core id		: 4 //4
core id		: 8 //5
core id		: 8 //6
core id		: 12 //7
core id		: 12 //8
core id		: 16 //9
core id		: 16 //10
core id		: 20 //11
core id		: 20 //12
core id		: 24 //13
core id		: 24 //14
core id		: 28 //15
core id		: 28 //16
core id		: 32 //17
core id		: 33 //18
core id		: 34 //19
core id		: 35 //20
core id		: 36 //21
core id		: 37 //22
core id		: 38 //23
core id		: 39 //24
```
P코어와 E코어 총합 24개가 나오는 모습입니다.
***
# Memory Usage
```
free -m
```
/               total        used        free      shared  buff/cache   available
Mem:            1967         505         914           2         706        1462
Swap:            951           0         951
***
NAME                    MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINTS
sda                       8:0    0   20G  0 disk  
├─sda1                    8:1    0  476M  0 part  /boot
├─sda2                    8:2    0    1K  0 part  
└─sda5                    8:5    0 19.5G  0 part  
  └─sda5_crypt          254:0    0 19.5G  0 crypt 
    ├─LVMGroup-root     254:1    0 11.2G  0 lvm   /
    ├─**LVMGroup-swap     254:2    0  952M  0 lvm   [SWAP]**
    ├─LVMGroup-home     254:3    0  952M  0 lvm   /home
    ├─LVMGroup-var      254:4    0  2.3G  0 lvm   /var
    ├─LVMGroup-srv      254:5    0  952M  0 lvm   /srv
    ├─LVMGroup-tmp      254:6    0  952M  0 lvm   /tmp
    └─LVMGroup-var--log 254:7    0  2.3G  0 lvm   /var/log
sr0                      11:0    1 1024M  0 rom   
***
메가바이트 단위로 메모리 사용량을 나타낸다.
여기서 swap 은 swap 메모리를 나타내며 이는 하드 용량이기 때문에 계산하지 않는다.
lsblk를 통해 확인한 swap과 용량이 거의 동일하다.
***
# Disk usage
```
df -BM
```
여기서 -B 옵션은 블록 사이즈를 나타낸다.
-BM을 주게되면 GB 단위로 표시하게 된다.