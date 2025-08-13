[도움되는 글](https://velog.io/@kafkaaaa/Linux-TTY)

콘솔, 터미널, tty는 서로 깊은 연관을 갖고 있는데 본래 이것들은 컴퓨터와 상호작용을 위한 장비를 뜻한다. 

unix시스템의 기본적인 이용방법은 unix가 인스톨된 호스트에 네트워크를 통해서 다른 컴퓨터가 접속하여 작업을
수행하는 것이다. 사용자는 단말에 명령을 넣어서 호스트를 조작하는데 이때 사용자로부터 명령을 받아서 호스트에
 전달하는 역활을 콘솔(console)이라고 한다. 
#### console이란?

컴퓨터를 조작할 때 사용하는 입출력 장치를 콘솔이라고 하고 명령조작에 사용하는 애플리케이션이나 OS자체를
   콘솔 또는 콘솔애플리케이션이라고 하는데 보통 많은 사람들이 콘솔이라고 부른다.
   또한  우리가 많이 사용하는 cmd도 콘솔이고 사용하는 터미널도 콘솔이다. 

  

**터미널**은 콘솔의 한 종류로 UI(Ctrl+Alt+T)로 사용할 수 있게 해주는 GUI(Graphic user interface) 프로그램이다. 일반적으로 키보드와 디스플레이로 구성된다. 조금 쉽게 말하면
터미널도 콘솔의 일부라고 보면 되며 윈도우에서는 명령프로토콜(cmd)이라고도 한다.

![](https://t1.daumcdn.net/cfile/tistory/2179364459603CA21C)

[출처] [http://www.linusakesson.net/programming/tty/](http://www.linusakesson.net/programming/tty/)

**TTY**도 콘솔의 한 종류로 Ctrl-Alt-F1 ~ F6 키조합으로 사용할수있는 OS 에서 제공하는 가상콘솔 이다. 실제 물리적인 장치가 연결된것이 아니기 때문에 커널에서 터미널을 emulation 한다. Line discipline, TTY driver 의 기능은 위와같고 마찬가지로 백그라운드 getty 프로세스에의해 login prompt 가 제공됩니다. /dev/tty[번호] 파일이 사용된다. TTY화면간 이동은 ALT+F1~F6이며 GUI환경 복귀는 ALT+F7이다.