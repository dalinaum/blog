최근에 리눅스 / 맥에서 펄 배포판은 `perlbrew`가 대세인 것 같습니다. 여러 버전을 로컬에 설치해서 관리할 수 있다는 것이 장점이 아닌가 싶고요. 특히 맥에선 mac ports등의 제품이 거지같이 펄을 패키징해두었고 요즘의 대세가 되고 있는 homebrew는 이미 맥에 설치된 프로그램에 대한 패키지를 제공하지 않는다는 정책을 가지고 있어서 대안이 없는 것 같습니다. (레거시에 의해 python과 ruby는 새 버전이 같이 패키징이 되어 있는 것 같은데 부럽습니다.)

이제 `perlbrew`를 설치합니다. `cpan`에서 받는 방법도 있지만 새 `perl`을 설치할 때까지 `cpan`은 순결하게 두겠습니다.
 
    curl -L http://xrl.us/perlbrewinstall | bash

초기화 과정이 필요합니다. `perlbrew`는 펄을 홈 디렉토리에만 여러 버전을 설치합니다. 그러니 모든 과정은 로컬 계정으로 진행합니다.
    
    ~/perl5/perlbrew/etc/perlbrew init

`.bash_profile`에 추가합니다.

    source ~/perl5/perlbrew/etc/bashrc

다음 터미널부터 perlbrew와 기타 perl등이 제대로 연결되어 수행됩니다.     

    perlbrew install perl-5.12.2

perl-5.12.2를 설치합니다.     

    perlbrew list

두가지 버전의 펄이 설치된 것을 볼 수 있습니다. 하나는 원래 맥에 있던 버전입니다. 놀랍게도 5.10인데요. mac ports 등을 깔면 이를 5.8버전으로 다운그레이드 시켜버립니다. (아까 말했던 mac ports의 거지같음이 이것입니다.)

다른 버전을 설치하거나 두가지 버전을 교체하면서 쓰는 방법은 `perlbrew` 엔터를 치면 쉽게 알 수 있을 겁니다.