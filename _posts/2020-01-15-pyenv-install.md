---
title: "pyenv 설치 및 사용법"
date: 2019-11-13 14:34:00
categories: python
---

## Mac에서 pyenv 설치 방법

### Homebrew를 이용하여, pyenv 설치

brew를 이용해 pyenv와 pyenv-virtualenv를 설치한다. 
brew 설치 관련은 이전 포스트[터미널 설정](https://swhur.github.io/terminal/terminal-setting/)을 참고하면 된다.

```

설치 후 pyenv관련 설정을 shell설정 파일에 추가
pyenv및 pyenv-virtualenv가 정상동작 할 수 있도록, 셸의 설정파일에 각 프로그램의 초기화 코드를 추가해야 합니다.

macOS와 Ubuntu에서는 기본 셸로 bash를 사용합니다.
셸의 설정파일은 ~/.bash_profile파일을 사용하며, ~/.bashrc파일을 사용하는 경우도 있습니다. 어떤 설정파일을 사용하는지는 pyenv를 설치한 후 터미널에 나타나니, 해당 메시지를 주의하여 보고 아래 과정을 따라합니다.

만약 zsh을 쓴다면 ~/.zshrc에 설정해주어야 합니다. 설치 후 터미널에 나타나는 메시지가 사용하는 셸의 종류에 따라 자동으로 변경됩니다.

아래 메시지는 Ubuntu에서 lhy사용자가 pyenv를 설치 완료 한 후 나타나는 메시지 예제입니다.