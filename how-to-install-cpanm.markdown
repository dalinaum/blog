펄이 설치되지 않은 윈도우즈 환경에 펄을 설치하려면 어떻게 해야할까? 신 버전 펄, 로컬 모듈, 현대적인 패키징 시스템을 함께 설치해보자.

먼저 [스트로베리 펄](http://strawberryperl.com/)을 받는다. 스트로베리 펄은 윈도우즈용으로 패키징된 펄에 [Bundle::CPAN](http://search.cpan.org/~andk/Bundle-CPAN-1.858/CPAN.pm), [Bundle:LWP](http://search.cpan.org/~gaas/libwww-perl-5.837/lib/Bundle/LWP.pm) 등의 모듈과 MinGW 개발 환경을 포함한 것이다. 인스톨러가 있으니 다운받아 설치하자.

다음으로 모듈을 로컬에 깔기 위해 [lib::local](http://search.cpan.org/~apeiron/local-lib-1.008001/lib/local/lib.pm)을 설치하고, 현대적인 패키징 [cpanm](http://search.cpan.org/~miyagawa/App-cpanminus-1.1008/bin/cpanm)을 설치할 차례다.

먼저 임시로 쓸 cpanm이 필요하다. [http://cpanmin.us](http://cpanmin.us)을 `cpanm`으로 저장한 후 다음 커맨드를 입력하자.

    perl cpanm --local-lib=~/perl5 local::lib App::cpanminus

로컬에 모듈을 설치한 것이기 때문에 추가적인 환경설정이 필요하다. 먼저 임시로 환경 변수를 추가하자.

    perl -Mlocal::lib > %TEMP%\tmp.bat && %TEMP%\tmp.bat && del %TEMP%\tmp.bat


영속적인 환경 설정을 위해 아래의 명령을 입력한다.

    llw32helper

앞으로 모듈을 로컬에 설치할 것이냐 묻는 질문에 `y`를 선택하였고 디렉토리는 디폴트로 하였다. 이렇게 설정된 환경은 재부팅 후에 적용된다.

설치가 제대로 되었는지 확인하기 위해 `cpanm`을 입력해본다. 임시로 설정된 환경 변수 때문에 제대로 작동할 것이다.

    cpanm
    
설치가 제대로 완료된지 확인한 후 처음 받았던 `cpanm`을 지운다.

    del cpanm

설치된 모듈 전체를 뽑아 업데이트하거나 로컬 영역에 설치한다.
    
    perl -MExtUtils::Installed -le "print for ExtUtils::Installed->new->modules" > modules
    type modules | perl -pe "system \"cpanm -v $_\""

그리고 개인적인 취향 때문에 `ack`를 설치했다. `ack`는 조금 더 현대적인 `grep` 구현이다.

    cpanm -f ack

굳이 `-f` 옵션을 붙인 건 윈도우즈에서 테스트 하나를 통과하지 못하기 때문이다. 그래도 사용에는 별 문제가 없어 설치했다.

위의 과정이 모두 자동화되었으면 좋겠지만 `cpanm`과 `local::lib` 등의 도구가 원래 펄 고유의 것이 아니기 때문에 공식 배포판에 포함될 수 없는 점이 아쉽다.
