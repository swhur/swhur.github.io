---
title: "anaconda3 클린 삭제"
date: 2019-11-13 14:34:00
categories: anaconda3
---

## Mac에서 anaconda3 클린 삭제 방법

### Anaconda Navigator를 삭제

Application에서 Anaconda Navigator를 휴지통으로 이동 시킨다. 
(주의. Anaconda Navigator가 실행 중이라면, 종료 후에 휴지통으로 이동 시켜야 한다.)


### Library 폴더의 파일 삭제

```
~/Library/Receipts/io.continuum.pkg.anaconda-client.bom
~/Library/Receipts/io.continuum.pkg.anaconda-client.plist
~/Library/Receipts/io.continuum.pkg.anaconda-navigator.bom
~/Library/Receipts/io.continuum.pkg.anaconda-navigator.plist
~/Library/Receipts/io.continuum.pkg.anaconda-project.bom
~/Library/Receipts/io.continuum.pkg.anaconda-project.plist
~/Library/Receipts/io.continuum.pkg.anaconda.bom
~/Library/Receipts/io.continuum.pkg.anaconda.plist
```
의 파일을 삭제한다.


### Anaconda3를 삭제한다. 

설치된 anaconda3 파일들을 삭제한다. 
(~/opt/anaconda3 에 설치되어 있어서 아래 명령어로 삭제)

```console
$ rm -rf ~/opt/anaconda3
```


### 블필요한 파일들 삭제

```console
$ rm  -rf ~/.condarc
$ rm  -rf ~/.conda
$ rm  -rf ~/.anaconda
```

### .zshrc 파일 수정

경로로 잡혀 있는 anaconda3를 제거한다.
