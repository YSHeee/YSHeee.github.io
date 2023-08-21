### :material-numeric-1-box-outline: <[Iterm2 커스텀](https://ooeunz.tistory.com/21)>

1. Iterm2 설치 [Iterm2](https://iterm2.com/)
2. Homebrew 설치 [Install-Homebrew](https://brew.sh/)
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
3. Homebrew **PATH** 추가
```bash
(echo; echo 'eval "$(/opt/homebrew/bin/brew shellenv)"") » /Users/_name_/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```
4. zsh 설치
```bash
brew install zsh
```
5. oh-my-zsh 설치 [Install-oh-my-zsh](https://github.com/ohmyzsh/ohmyzsh)
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
6. Iterm2에 Color theme 적용 [Palette](https://iterm2colorschemes.com/)
```bash 
# Example
curl -LO https://raw.githubusercontent.com/mbadolato/iTerm2-Color-Schemes/master/schemes/3024%20Day.itermcolors
```
iTerm2 > Preference > Profiles > Colors > Color Presets > import
7. 폰트 변경 [D2](https://github.com/naver/d2codingfont)<br>
    - iterm: iTerm2 > Preference > Profiles > Text > Font
    - mac terminal: 터미널 > 환경설정 > 프로파일 > 서체
8. 테마 변경
```bash 
vi ~/.zshrc
# ZSH_THEME="robbyrussell" -> agnoster
# esc+wq!
```
9. 상태바
    - 상태바 추가: iTerm2 > Preferences > Profiles > Session > Status bar enabled 
    - 상태바 위치: Preferences > Appearance > Status bar location > Bottom 
10. Plugin
```bash 
brew install zsh-sysntax-highlighting
vi ~/.zshrc
source /opt/homebrew/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

brew install zsh-autosuggestions
vi ~/.zshrc
source /opt/homebrew/share/zsh-autosuggestions/zsh-autosuggestions.zsh
```
11. Alias +ll
```bash 
vi ~/.bash_profile
# alias ll="ls -a" 추가
```


### :material-numeric-2-box-outline: Python Setting
1. Miniconda 설치 [Install-Miniconda](https://docs.conda.io/en/latest/miniconda.html)
```bash 
brew install wget
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.sh
bash Miniconda3-latest-MacOSX-x86_64.sh
```
2. Vscode Python Extension 설치
3. Vscode Jupyter Extension 설치

### :material-numeric-3-box-outline: Java Setting
1. JDK 설치 [Install-java](https://www.oracle.com/kr/java/technologies/downloads/#java11-mac)
2. Vscode Extension Pack for Java 설치
3. Code > Preferebces > Settings > "java home" 검색 > Edit in settings.json > /Library/Java/JavaVirtualMachines/.../Home 삽입 
