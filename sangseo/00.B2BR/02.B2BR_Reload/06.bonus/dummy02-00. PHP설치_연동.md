![[Pasted image 20240417213309.png]]
php를 설치하기 위해서는 ppa를 사용해야 합니다. ppa는 Personal Package Archive의 약자로 개인이 관련 자료를 올려놓은 저장소를 말합니다.

아마 이전 버젼의 php 설치 시 등록했을지 모르지만 다시 ppa(Personal Package Archive)를 등록해 줍니다.

php 설치 시 사용하는 ppa는 [Ondřej Surý의 개인 저장소](https://launchpad.net/~ondrej/+ppa-packages) 가 가장 유명하고 많이 사용됩니다. 여기서도 Ondřej Surý의 개인 저장소를 이용할 것입니다.

이는 아래와 같은 명령을 사용해 PHP 저장소 추가 및 보안키 등록합니다.
```
apt-get install software-properties-common && add-apt-repository ppa:ondrej/php
```
