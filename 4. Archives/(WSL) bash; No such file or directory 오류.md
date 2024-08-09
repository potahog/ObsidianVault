# [WSL, Terminal] -/usr/bin/env: 'bash\r': No such file or directory 오류

오류 메시지
```bash
/usr/bin/env: ‘bash\r’: No such file or directory
```
문제 상황
llama3 모델 다운로드를 하기 위해서 download.sh 셀 스크립트를 실행하려고 했지만 위의 상황이 발생함.
윈도우와 Mac/Linux 상에서 개행 문자가 서로 **CRLF(\r\n)**, **LF(\n)** 로 달라 발생한 문제라고 함.

1. 해결1
	 WSL을 껐다가 다시 키면 자동으로 해결된다고 함.
	 Powershell
``` shell
wsl --shutdown
wsl
```
2. 해결2
	 위의 상황에서 해결이 되지 않으면 WSL 상에서 /etc/wsl.conf 파일을 수정해야 한다고 함.
```shell
sudo nano /etc/wsl.conf
// or
sudo vi /etc/wsl.conf
```
	로 아래 문장을 넣고 수정을 하면 된다.
``` text
[interop]
appendWindowsPath = false
```
	 그리고 WSL을 종료한 다음에 Powershell에서 WSL을 재실행 주면 된다.
```shell
wsl --shutdown
wsl
```
3. 해결 3
	위의 방법으로도 안된다면 파일을 수정하는 방법으로 실행해야한다. 스크립트에 Windows 스타일 \r\n줄 끝을 \r으로 변경해줘야 한다.
``` bash
sudo sed $'s/\r$//' [file name] > [modify file name]
```
	 이후에 아래 문구로 실행하면 된다.
```bash
./[file name] --clang-completer
```
--------------------------------------------------
#### Reference
[잭무의 개발새발](https://wondev.tistory.com/73)
[stackoverflow env:bash\r:No such file or directory](https://stackoverflow.com/questions/29045140/env-bash-r-no-such-file-or-directory)
#WSL #bash