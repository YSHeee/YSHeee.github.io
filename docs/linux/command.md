# Linux Command

# 🛠️🛠️🛠️...🛠️🛠️🛠️🏚️

|    Command    |    Description   |    Option    |
| :-----------: | :-----------: | :-------------- |
ls  |   해당 dir 안의 모든 파일/폴더 출력
ls -l   |   해당 dir 안의 모든 파일/폴더를 리스트로 출력
ls -al  |   숨겨진 파일/폴더까지 출력
mkdir   |   dir생성
cd  |   dir 들어가기
cd.. |  이전 dir 들어가기
pwd |   해당 위치를 절대 경로로 반환
rm -r `dir_name`    |   해당 dir 삭제
netstat |   포트 확인
grep    |   입력으로 전달된 파일의 내용에서 특정 문자열을 찾고자할 때 사용
df -h   |   GB 단위로 용량 확인
du -h   |   현 dir에서 서브 dir까지의 사용량 확인 (GB)
du -h --max-depth=1    |   폴더별 용량 확인
ps -ef  |   동작 중인 프로세스 확인



---

### zip 파일 압축 해제
``` bash
unzip file_name.zip -d path # 해제
``` 

### tar 파일 압축/해제
- `.tgz`, `.targz` : 압축된 tar 아카이브의 일반적인 파일 확장자
- `.tar` : 아카이브가 압축되지 않은 경우의 확장자
=== "압축"
    ``` bash
    tar -czvf file_name.tgz path
    tar -zcvf aaa.tar.gz abc #example
    ```
=== "해제"
    ```bash
    tar -xvf file_name.tgz
    tar -zxvf aaa.tar.gz #example
    ```
- `c` : 
- `z` : 
- `v` : 
- `f` : 
- `x` : 

---

### 파일 원격 전송
- **local ⇒ remote** 파일 전송
    - scp [option] [file_name] [remote_id]@[remote_IP]:[file을 받을 위치]
``` bash
scp filepath/filmname remoteID@remoteIP:file_path
```
- **remote ⇒ local** 파일 전송
    - scp [option] [remote_id]@[remote_IP]:[file_path] [file을 받을 위치]
``` bash title="로컬에서 실행 시"
scp hostID@hostIP:dirpath/filename local_path
```

- **local ⇒ remote** 디렉토리와 그 하위 파일까지 모두 전송
    - scp -r [dir_path] [remote_id]@[remote_IP]:[받을 위치]
``` bash
scp -r dirpath remoteID@remoteIP:전송된 파일이 들어갈 경로
```
- **remote ⇒ local** 디렉토리와 그 하위 파일까지 모두 전송
    - scp -r [remote_id]@[remote_IP]:[가져올 dir 위치] [받을 위치] 
``` bash title="로컬에서 실행 시"
scp -r remoteID@remoteIP:dirpath local_dir_path
```

- rsync

---