# [tmux](https://tmuxguide.readthedocs.io/en/latest/tmux/tmux.html)

`apt-get install tmux`

|    Command    |    Description   |  
| :-----------: | :-----------: | 
tmux    |   실행. 세션 생성
tmux new -s <session_name>  |   해당 세션 생성
Ctrl+b 그리고 d |   detached ( 해당 세션 백그라운드)
tmux attach |   (백그라운드 상태의) tmux 세션 활성화
tmux attach -t session_name |   해당 sesson 활성화
tmux ls |   세션 리스트
Ctrl+d  |   세션 닫기
Ctrl+b 그리고 “ |   상-하 창 나누기
Ctrl+b 그리고 % |   좌-우 창 나누기
exit    |   세션 종료 (세션 내에서)
tmux kill session -t session_name   |   세션 종료 (세션 바깥에서)


- You can do pkill -USR1 tmux to make it create the socket again.
