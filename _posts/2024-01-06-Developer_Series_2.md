---
title: Windows에서 Linux 개발 환경 구축하기 시리즈 2 (WSL2 설치 및 Oracle Linux 설치)
date: YYYY-MM-DD HH:MM:DD +09:00
categories: [Linux]
tags: [windows, windows11, wsl, Linux, C, Golang, Docker, Kuberntes, oh-my-zsh, WSL2]     # TAG names should always be lowercase
---

## 목표 

안녕하세요. Winey 입니다.<br>
이번에는 Windows11에서 WSL2를 설치 하고 Oracle Linux 설치 방법에 대해서 공유 하려고 합니다.<br>
<br>

---

## WSL2 설치
Windows11에서는 단순히 아래 명령어를 `PowerShell`에서 수행하면 된다.<br>
> 주의 할 점은 PowerShell 실행 시 관리자 권한으로 실행 해야 한다는 점이다.<br>    

```
% wsl --install
```

---

## Oracle Linux 설치 이유 
wsl 처음 설치 했다면 기본 배포판으로 Ubuntu(Debian 기반)가 설치 되어 있을 것이다. <br>
그러나 실제 상용 운영 환경에서는 Ubuntu 보다는 Red Hat 계열의 Linux를 많이 사용 한다. <br>
Red Hat 계열의 대표 적인 Linux는 `Red Hat Enterprise Linux`, `CentOS`, `Oracle Linux` , `SUSE Linux` 다. <br>
<br>
특징은 간단히 표현하자면 아래와 같다. (물론 개인적인 의견이 들어가 있을 수 있습니다.)
* Red Hat Enterprise Linux
  * 유료다 ..
* CentOS
  * 지원이 종료 된다.
* Oracle Linux (wsl에서 설치 가능)
  * 무난해 보인다.
* SUSE Linux
  * 유럽에서 많이 사용된다는 풍문.. 
<br>

제일 무난해 보이기 때문에 Oracle Linux를 설치해보려고 한다.<br>
<br>

---

## Oracle Linux 설치
먼저 설치 가능한 Linux 리스트를 조회하면 아래의 명령어를 수행 하면 된다.
> PowerShell 관리자 권한으로 실행 하세요.

```
PS C:\WINDOWS\system32> wsl -l -o

NAME                                   FRIENDLY NAME
Ubuntu                                 Ubuntu
Debian                                 Debian GNU/Linux
kali-linux                             Kali Linux Rolling
Ubuntu-18.04                           Ubuntu 18.04 LTS
Ubuntu-20.04                           Ubuntu 20.04 LTS
Ubuntu-22.04                           Ubuntu 22.04 LTS
OracleLinux_7_9                        Oracle Linux 7.9
OracleLinux_8_7                        Oracle Linux 8.7
OracleLinux_9_1                        Oracle Linux 9.1
openSUSE-Leap-15.5                     openSUSE Leap 15.5
SUSE-Linux-Enterprise-Server-15-SP4    SUSE Linux Enterprise Server 15 SP4
SUSE-Linux-Enterprise-15-SP5           SUSE Linux Enterprise 15 SP5
openSUSE-Tumbleweed                    openSUSE Tumbleweed
```

설치하려는 Oracle Linux 버전을 확인 후 아래의 명령어로 설치 하면 된다.

```
PS C:\WINDOWS\system32> wsl --install -d  OracleLinux_9_1
설치 중: Oracle Linux 9.1
Oracle Linux 9.1이(가) 설치되었습니다.
Oracle Linux 9.1 실행 중...
```

설치가 완료되었다면 Oracle Linux Terminal 창이 열 릴 것이다.
```
Installing, this may take a few minutes...
Please create a default UNIX user account. The username does not need to match your Windows username.
For more information visit: https://aka.ms/wslusers
Enter new UNIX username:
```

계정 명과 비밀번호를 입력하면 설치 끝!
```
Installing, this may take a few minutes...
Please create a default UNIX user account. The username does not need to match your Windows username.
For more information visit: https://aka.ms/wslusers
Enter new UNIX username: ####
Changing password for user ####.
New password:
BAD PASSWORD: The password contains the user name in some form
Retype new password:
passwd: all authentication tokens updated successfully.
Installation successful!
이제 Linux용 Windows 하위 시스템을 Microsoft Store에서 사용할 수 있습니다.
'wsl.exe --update'를 실행하거나 https://aka.ms/wslstorepage를 방문하여 업그레이드할 수 있습니다.
Microsoft Store의 WSL을 설치하면 최신 WSL 업데이트가 더 빠르게 제공됩니다.
자세한 내용은 https://aka.ms/wslstoreinfo를 방문하세요.
```
---

## 마무리
무언가를 ... 설치하고 설정하는 과정이 순탄했던 기억이 없는데 공식 홈페이지에서 소개되는 내용만으로 설치 된 적은 처음인 것 같다.<br>
포스팅을 하는 입장에서는 다양한 오류가 발생해야 해결하는 것도 포스팅을 할텐데 ... 이렇게 또 무난하게 넘어간 적은 처음이라 당황하는 중이다. <br>
<br>
~~그렇다고 앞으로 작성할 시리즈에서 오류 왕창 났으면 하는 마음은 아니다.~~

자 그럼 다음 포스팅에서는 `oh-my-zsh`설치 및 설정 방법과 Theme 설정 방법에 대해서 설명 하겠습니다.
---

## 시리즈
* Windows에서 Linux 개발 환경 구축하기 시리즈 1 (시작하며)
* Windows에서 Linux 개발 환경 구축하기 시리즈 2 (WSL2 설치 및 Oracle Linux 설치)
* Windows에서 Linux 개발 환경 구축하기 시리즈 3 (oh-my-zsh 설치 및 theme 설치)
* Windows에서 Linux 개발 환경 구축하기 시리즈 4 (C 개발 환경 꾸리기)
* Windows에서 Linux 개발 환경 구축하기 시리즈 5 (Golang 개발 환경 꾸리기)
* Windows에서 Linux 개발 환경 구축하기 시리즈 6 (docker,kubernetes 관련 명령어 설치)

---
