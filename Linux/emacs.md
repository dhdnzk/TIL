### 이맥스 삽질기

#### 설치한 플러그인 목록

- evil-mode (vim 사용자라면 필수!)
- org-mode (스케쥴러)
- powerline
- eclim (자바 개발환경)
- elpy (파이썬 개발환경)
- js2-mode (javascript 개발환경)
- spacemacs(evil-mode, org-mode, powerline등 자동으로 내장되있어서 적응기동안 사용하기 좋을듯!)

#### TIPS

- 기본적으로 이맥스는 ~/.emacs 파일에 초기화 설정을 입력해 주지만, spacemacs를 사용한다면 ~/.spacemacs 파일 안에 초기화 설정을 해주는 함수가 있음. 여기에다 설정해주자!
- spacemacs를 사용하는데 홈디렉터리에 ~/.emacs 파일도 있다면, 이맥스 실행시에 spacemacs가 실행되지 않고 ~/.emacs파일로 초기화가 됨.
- scratch 버퍼는 아무 옵션도 없이 vi를 열었을 때 처럼 낙서장같은개념 
- evil-mode 를 사용하고 있다면, 어떤 미니버퍼든지 :e /경로/파일명 을 통해서 현재 버퍼에 있는 텍스트 내용을 저장해 줄 수 있음(굿)
- elisp 언어의 특징 : (함수명 매개변수1 매개변수2 ... 매개변수n)의 형식
- 특정 모드를 실행시킨다던지 어떤 기능에 대한 단축키가 생각나지 않을때는.. 'M-x 명령이름'으로 검색하자
- spacemacs에서는 M-x을 누르면 사용 가능한 명령어 리스트와 자동완성 기능이 나오는데, 이 패키지 이름 : helm 

#### Package Management
 - install-package 를 통해서 플러그인을 설치할 경우에, 이맥스를 재시작하면 설치한 패키지를 검색해도 나오지 않는다.
 - 이는 버그가 아니라 의도된 기능이고, ~/.spacemacs파일에서 다음 함수에 package 이름을 추가하면 이맥스롤 재시작해도 자동으로 추가가 되있음
 
 - ~/.spacemacs
 ```elisp
 
 (defun dotspacemacs/layers ()
 
   dotspacemacs-additional-packages '(
                                      ;;여기에 추가!
                                     )

 )

 ```

#### issue

- M-x package-list 에서 간단하게 플러그인 설치가 가능한데, 이맥스 종료 후에 재접속해보면 전부 사라져있음..(Tips의 Package MAnagement 섹션에 추가 내용 설명해둠)
- emacs 안에서 eshell이나 ansi-term 을 실행시키고, 그 안에서 vi명령어로 파일을 열면 파일도 깨지고, 특히나 evil-mode상태라면 명령행모드로 들어갈 수가 없다!(혹시 잘못열면 C-x k 미니버퍼 kill을 통해서 나가주자)
- emacs 안에서 tmux를 사용하고 싶은데, 실행이 안됨. 역으로 터미널 열고 tmux를 실행해서 그 안에서 emacs를 열어도 단축키가 겹쳐서 제대로 동작하지 않음..

#### references

- [http://jr0cket.co.uk/2015/08/spacemacs-first-impressions-from-an-emacs-driven-developer.html](http://jr0cket.co.uk/2015/08/spacemacs-first-impressions-from-an-emacs-driven-developer.html)
- [http://blog.nacyot.com/articles/2014-03-12-emacs-with-tern/](http://blog.nacyot.com/articles/2014-03-12-emacs-with-tern/)
