---
title: "터미널 설정"
date: 2019-11-06 13:04:00
categories: terminal
---

## 터미널 설정 배경
기본적으로 제공하는 터미널을 사용해도 되지만, 좀 더 편하고 효율적인 사용을 위해서 터미널을 설정한다. (iterm2 사용)
새로 설치된 맥(Catalina 기준)에는 기본적으로 zsh를 사용하도록 되어 있다. (bash를 사용하는지 알았는데 아님)
터미널 확인은 다음 명령어로 확인 가능하다.  
```console
$ echo $SHELL
``` 

## 터미널 설정
Oh My ZSH와 iterm2의 조합으로 터미널을 설정한다. 
[Oh My ZSH+ iTerm2로 터미널을 더 강력하게](https://medium.com/harrythegreat/oh-my-zsh-iterm2%EB%A1%9C-%ED%84%B0%EB%AF%B8%EB%84%90%EC%9D%84-%EB%8D%94-%EA%B0%95%EB%A0%A5%ED%95%98%EA%B2%8C-a105f2c01bec)을 참고하였음

### iterm2 설치
[iterm2 site](https://www.iterm2.com/)에서 최신 버전을 다운 받아서 설치한다.

### iterm2 컬러 설정 변경
[iTerm2-Color-Schemes](https://github.com/mbadolato/iTerm2-Color-Schemes)에서 컬러 설정을 다운 받아서, iterm2에 import 후 설정한다.
iTerm2 -> Profiles -> Open Profiles -> Edit Profile -> Colors -> Colors Presets -> Import 에서 다운 받은 Schemes를 전체 선택한다. 
(나중에 바꿀수가 있으므로 전체 import)

### Homebrew 설치
Homebrew는 mac os용 패키지 관리 어플리케이션이다. 
설치는 아래 명령어를 수행하면 된다.
```console
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
``` 

### zsh 설치
brew를 통하여 최신 버전의 zsh를 설치한다. 
```console
$ brew install zsh
``` 

### Oh My ZSH 설치
Oh My ZSH는 zsh를 더 쉽게 사용할 수 있게 해주는 플러그 인으로서, 아래 명령어로 설치하면 된다. 
```console
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
``` 

### 터미널 꾸미기
#### 테마 설정
agnoster 테마를 설정한다. .zshrc 파일을 열어서, ZSH_THEME=”robyrussell” 부분의 robyrussell을 agnoster로 변경한다.

#### 폰트 설정
naver에서 제공하는 NanumGothic 폰트와 D2Coding 폰트를 설치한다. 
(폰트 설정 부분은 따로 작성할려고 했으나, 터미널 설정에 필요하므로 여기서 작성)

##### 폰트 설치
[나눔고딕폰트](https://hangeul.naver.com/font)에서 폰트를 다운받아서 설치한다. 
[D2Coding폰트](https://github.com/naver/d2codingfont)에서 폰트를 다운받아서 설치한다. 
설치 방법은 다운 받은 파일을 /Library/Fonts에 복사하면 된다. 

##### iterm2에 폰트 설정
iTerm2 -> Profiles -> Open Profiles -> Edit Profile -> Text -> Font -> D2Coding 선택

#### prompt text 변경
.zshrc 파일 하단에 다음의 문구를 추가한다. 
prompt_context() {
  if [[ "$USER" != "$DEFAULT_USER" || -n "$SSH_CLIENT" ]]; then
    prompt_segment black default "%(!.%{%F{yellow}%}.)$USER"
  fi
}

#### new line 적용하기
theme 파일을 열어서, prompt_newline 함수를 추가한다. 
```
prompt_newline() {
  if [[ -n $CURRENT_BG ]]; then
    echo -n "%{%k%F{$CURRENT_BG}%}$SEGMENT_SEPARATOR
%{%k%F{blue}%}$SEGMENT_SEPARATOR"
  else
    echo -n "%{%k%}"
  fi

  echo -n "%{%f%}"
  CURRENT_BG=''
}
```
그 이후에 build_prompt 함수를 수정한다. 
```
build_prompt() {
  RETVAL=$?
  prompt_status
  prompt_virtualenv
  prompt_context
  prompt_dir
  prompt_git
  prompt_bzr
  prompt_hg
  prompt_newline // 추가
  prompt_end
}
```
그런데 이 부분은 필요가 없을 듯 해서, build_prompt는 추가하지 않음

#### Syntax Hightlight 적용
brew를 통하여 설치한다. 아래의 명령어를 수행하면 된다. 
```console
brew install zsh-syntax-highlighting
```
그 이후에, 플러그인을 적용한다. 
```console
source /usr/local/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
```

이상으로 iterm2 터미널 설정을 마친다.

