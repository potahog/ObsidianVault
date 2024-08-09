---
title: Obsidian 데스크탑 메뉴 만들기
OS:
  - Linux
  - Rocky Linux
reference_url:
  - https://nomad-programmer.tistory.com/525
tags:
  - Linux
  - desktop_file
  - obsidian
---
## Resource
### .desktop file
```
[Desktop Entry]
Name=Obsidian
Exec=/home/user/apps/obsidian/Obsidian-1.4.14.AppImage %u
Terminal=false
Type=Application
Icon=/home/user/apps/obsidian/obsidian.png
StartupWMClass=obsidian
X-AppImage-Version=1.4.14
Comment=Obsidian
Categories=Office;
MimeType=text/html;x-scheme-handler/obsidian;
```

### icon
[![Obsidian Image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbffdxh%2Fbtsxp7tCxUL%2FZQedxXkEK0q8Gpmnzwaenk%2Fimg.png)]
