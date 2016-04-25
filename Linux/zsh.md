### ZSH 사용하기

#### zsh 설치여부 확인

```
zsh --version
```

#### 기본 쉘 zsh로 변경

```
chsh -s `which zsh`
```

#### oh-my-zsh 설치

```
curl -L https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh | sh
```

#### theme 설정

- ~/.zshrc 에서 ZSH_THEME="" 수정
- 추천 테마 : ZSH_THEME="agnoster"
- 위에 테마 사용하기 위해 필요한 폰트 참조 페이지 : [https://github.com/powerline/fonts](https://github.com/powerline/fonts)
- 테마 종류 보려면 ~/.oh-my-zsh/themes/ 디렉터리 참고
