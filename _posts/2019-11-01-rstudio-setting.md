---
title: "RStudio 설정"
date: 2019-11-01 12:42:00
categories: RStudio
---

## RStudio 설정
### R 설치
[R site](https://cran.r-project.org/bin/macosx/)에서 맥용 R을 받아서 설치한다.

### RStudio 설치
[RStudio site](https://rstudio.com/products/rstudio/download/)에서 맥용 RStudio을 받아서 설치한다.

### Java 설치
자연어 처리 Library인 KoNLP 또는 NLP4Kec 등에서 한글을 사용하기 위해서는 rJava 패키지가 필요하다. 그런데, rJava 패키지는 java 설치가 필요하다.
java 설치 없이 library(rJava)을 실행 시에는 다음과 같은 에러가 출력된다. 
```
> library(rJava)
Unable to find any JVMs matching version "(null)".
No Java runtime present, try --request to install.
에러: package or namespace load failed for ‘rJava’:
 .onLoad가 loadNamespace()에서 'rJava'때문에 실패했습니다:
  호출: dyn.load(file, DLLpath = DLLpath, ...)
  에러: 공유된 객체 '/Library/Frameworks/R.framework/Versions/3.6/Resources/library/rJava/libs/rJava.so'를 로드 할 수 없습니다:
  dlopen(/Library/Frameworks/R.framework/Versions/3.6/Resources/library/rJava/libs/rJava.so, 6): Library not loaded: /Library/Java/JavaVirtualMachines/jdk-11.0.1.jdk/Contents/Home/lib/server/libjvm.dylib
  Referenced from: /Library/Frameworks/R.framework/Versions/3.6/Resources/library/rJava/libs/rJava.so
  Reason: image not found
추가정보: 경고메시지(들): 
In system("/usr/libexec/java_home", intern = TRUE) :
  명령 '/usr/libexec/java_home'의 실행으로 상태 1가 되었습니다
```
위의 에러를 해결하기 위해서는 java를 설치해야 한다 (java 8 버전을 설치한다. 상위 버전에서는 문제가 발생)
[오라클 site](https://www.oracle.com/technetwork/java/javase/downloads/index.html)에서 다운받아서 설치

심볼릭 링크를 생성한다.
```console
sudo ln -s $(/usr/libexec/java_home)/jre/lib/server/libjvm.dylib /usr/local/lib
```

```console
$ sudo R CMD javareconf
```

이 작업 이후에도, RStudio에서는 library(rJava)시에 오류가 발생한다. 
(R 에서는 정상동작 한다.)
해당 오류를 해결하기 위해서, 소스로 rJava를 설치하고자 한다. 

여기서 또 문제가 발생한다. 소스로 rJava를 설치할려고 하면 컴파일 에러가 발생한다. 
```
*** jdk is incomplete! please make sure you have a complete jdk. jre is *not* sufficient.
```

구글에서 검색한 결과 [해결방법](https://zhiyzuo.github.io/installation-rJava/)을 찾아냈다. 

해당 문제는 GUI 툴에서만 발생하는 이슈로서, jenv를 설치하여야 한다. (brew를 이용해서 설치한다.)
```console
$ brew install jenv
```

jenv 관련 설정을 .zshrc에 추가한다.
```
export PATH="$HOME/.jenv/bin:$PATH"
eval "$(jenv init -)"
```

.zshrc를 다시 읽어온다.
```console
$ source ~/.zshrc
```

java 환경을 추가한다. (설치 버전은 1.8.0_231)
```console
$ jenv add /Library/Java/JavaVirtualMachines/jdk1.8.0_231.jdk/Contents/Home
```

```
oracle64-1.8.0.231 added
1.8.0.231 added
1.8 added
```
이렇게 세개가 추가된다. 
oracle64-1.8.0.231만 사용하므로, 1.8.0.231, 1.8는 제거한다.
```console
$ jenv remove 1.8.0.231
$ jenv remove 1.8
```

gcc도 최신 버전으로 설치한다. (brew를 이용하여 설치)
Mac에 존재하는 gcc로는 다음과 같은 에러가 발생한다.
```
clang: error: unsupported option '-fopenmp'
make[2]: *** [libjri.jnilib] Error 1
make[1]: *** [src/JRI.jar] Error 2
make: *** [jri] Error 2
ERROR: compilation failed for package ‘rJava’
```

```console
brew install gcc
```

홈에 .R 디렉토리를 생성하고, Makevars 파일을 생성한다.
```console
$ mkdir ~/.R
$ cd ~/.R
$ vi Makevars
```

아래와 같이 파일을 편집한다.
```
CC=/usr/local/Cellar/gcc/9.2.0_1/bin/gcc-9
CXX=/usr/local/Cellar/gcc/9.2.0_1/bin/g++-9
CXX11=/usr/local/Cellar/gcc/9.2.0_1/bin/g++-9
CXX14=/usr/local/Cellar/gcc/9.2.0_1/bin/g++-9
cxx17=/usr/local/cellar/gcc/9.2.0_1/bin/g++-9
cxx1X=/usr/local/cellar/gcc/9.2.0_1/bin/g++-9
LDFLAGS=-L/usr/local/Cellar/gcc/9.2.0_1/lib
```

R java 설정을 다시 진행한다.
```console
$ sudo R CMD javareconf
```

소스 모드로 rJava를 설치한다.
```
install.packages("rJava", dependencies = TRUE, type = "source")
```

라이브러리를 로드한다.
```
library(rJava)
.jinit()
```
