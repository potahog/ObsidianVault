---
title: .desktop 파일 만들기
OS:
  - Linux
  - Rocky Linux
tags:
  - Linux
  - Rocky_Linux
  - OS
  - desktop_file
reference_url:
  - https://crasy.tistory.com/143
---
.desktop 파일은 /usr/share/applications 폴더에 존재해야한다.

.desktop 파일 첫 줄에는 \[Desktop Entry\]가 존재해야한다.

``` .desktop
[Desktop Entry]
Encoding=UTF-8
Version=1.0
Type=Application
Terminal=false
Exec=<<$Program Name Path>>
Icon=<<$Program Icon Path>>
```
 위는 .desktop에 들어가는 기본적인 내용이다

| desktop properties               | description                                                          |
| -------------------------------- | -------------------------------------------------------------------- |
| \[Desktop Entry\]                | .desktop 파일이 시작되는 지점                                                 |
| Encoding=UTF-8                   | 인코딩 설정                                                               |
| Version=1.0                      | .desktop파일의 버전                                                       |
| Name=Program Name                | 프로그램 이름                                                              |
| Comment=Program Description      | 프로그램 팁 혹은 간단한 설명. 시작메뉴에서 아이콘 위로 마우스 호버 상태에서 뜨는 툴팁 내용                 |
| Exec=Program Path %U             | 프로그램 위치. 환경 변수에 등록 되어있으면 프로그램 명만 적어도 됨. %U를 적어두면 파일을 연결 프로그램으로 설정 가능 |
| Icon=Program Icon Path           | 프로그램 아이콘 위치. 지원 포멧은 png, xpm, svg 이며 권장하는 포멧은 png                    |
| Terminal=false                   | 프로그램을 실행 시 터미널 실행 여부                                                 |
| Categories=Application           | 프로그램 타입 지정, Applicatio, Link, Directory...                           |
| StartupNotify=true;              | 프로그램 카테고리, 세미콜론으로 구분. 메뉴를 지원하는 데스크탑에서 카테고리 메뉴에 등장                    |
| Hidden=false                     | true이면 삭제된 프로그램같이 취급                                                 |
| OnlyShowIn                       |                                                                      |
| NotShowIn                        |                                                                      |
| MimeType                         | http://www.iana.org/assignments/media-types.xhtml (영문)               |
| path=Program Directory           | 프로그램의 작업 디렉토리 지정                                                     |
| NoDisplay=false                  | 프로그램이 존제하지만 메뉴에 나타나지 말아야 할때 true                                     |
| GenericName=Program Generic Name | 프로그램의 일반적인 이름                                                        |
| URL=URL Address                  | URL 접속                                                               |
| TryExec=Program Path             | 프로그램이 실제로 설치되어 있는지 확인하는데 사용                                          |
| Interface=Program Interface      | 프로글매에서 인터페이스를 지정해야하는 경우                                              |
|                                  |                                                                      |



##### Reference
[HELLO_HELL? - \[Linux\] .desktop 파일 만들기](https://crasy.tistory.com/143)
