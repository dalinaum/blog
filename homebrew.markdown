macports는 아래와 같은 단점이 있다.

0. [관리자 권한](http://guide.macports.org/#using.port)이 필요하다.
1. 기존의 맥에 설치된 프로그램을 이용하지 않아 컴파일 시간이 길고 설정을 망가트릴 수 있다.
2. 디폴트 패키징 버전이 나빠 심지어 디폴트 맥보다 구버전인 경우도 종종 있다.
3. 다른 버전으로 변경하려 할 때 [패키지를 망가트려 다시 설치하는 경우가 발생](http://dalinaum-kr.tumblr.com/post/2756330737/why-old-perl-in-macports)한다.
4. 여러 버전을 동시에 이용하는 것이 쉽지 않다.
5. [패키징을 만드는게 너무나 복잡](http://guide.macports.org/#development.creating-portfile)하다.

그래서 macports를 버리고,

    sudo port -f uninstall installed
    sudo rm -rf \
        /opt/local \
        /Applications/DarwinPorts \
        /Applications/MacPorts \
        /Library/LaunchDaemons/org.macports.* \
        /Library/Receipts/DarwinPorts*.pkg \
        /Library/Receipts/MacPorts*.pkg \
        /Library/StartupItems/DarwinPortsStartup \
        /Library/Tcl/darwinports1.0 \
        /Library/Tcl/macports1.0 \
        ~/.macports
    sudo rm -rf /usr/local
    sudo mkdir /usr/local
    chown `whoami` /usr/local

[homebrew](http://mxcl.github.com/homebrew/)로 갑니다. 당연히 homebrew는 위의 문제에서 해방되었습니다.

설치는 굉장히 쉽습니다. [XCode](https://connect.apple.com/)가 설치되어 있다면 아래와 같이 입력합니다.

    ruby -e "$(curl -fsSLk https://gist.github.com/raw/323731/install_homebrew.rb)"

맥에 있는 `ruby`와 `curl` 이용해서 설치가 진행됩니다. `.bash_profile`에서 `/usr/local/bin`을 PATH에 추가합니다.

이제 `wget`을 컴파일해봅시다.

    brew install wget

설치가 된 후에 아래와 같이 입력합니다.

    $ ls -l /usr/local/Cellar/wget/ 
    total 0
    drwxr-xr-x  9 dalinaum  wheel  306  1 27 01:47 1.12

개별 패키지 버전별로 디렉토리가 생성되는 것을 볼 수 있습니다. 언제든지 다른 버전으로 갈아탈 수 있습니다.

mercurial을 설치하고 싶어서 아래와 같이 입력했습니다.

    $ brew install hg
    Mercurial can be install thusly:
      brew install pip && pip install mercurial

놀랍게도 설치를 거부하고, 다른 방법을 사용하라고 합니다. homebrew는 기존에 맥에 있거나 별도의 패키징 시스템이 있다면 협력합니다. (python과 ruby는 예외적으로 인터프리터가 맥에 있지만 별도의 패키지로 존재하고 있습니다. 관리자는 그런 상황을 맘에 안들어 하는 것 같으니 언제 지워질지 모르지만요.)

homebrew는 많은 사람들이 패키지(포뮬러)를 제작합니다. [공식 github에서도 그 패키지](https://github.com/mxcl/homebrew/pulls)를 찾을 수 있고 다른 `git` 리포에서도 찾을 수 있습니다.

또, 포뮬러는 인터넷에 해당 프로그램에 대한 URI가 있다면 스스로 만들 수 있습니다. 이 과정은 매우 쉽습니다.

    brew create http://example.com/foo-0.1.tar.gz

이제 포뮬러의 얼개가 작성되었습니다. [버전 정보 등을 추가](https://github.com/mxcl/homebrew/wiki/Formula-Cookbook)하면 끝입니다. 포뮬러에 의해 설치된 프로그램은 별도의 디렉토리에서 다른 포뮬러와 별도로 관리됩니다!