# Local Git

## Git 준비

[Git 설치](https://www.notion.so/Git-8934e019ee2849b4968f21a24610818b?pvs=21) Git 

giti char값

이메일주소

타임스템프

커밋 메시지가 포홤되어야함

### Git 설치 확인

```bash
git version
```

### Git 최초 설정

```bash
git config --global user.name "<사용자 이름>"
git config --global user.email "email@email.com"
```

### Git 설정 확인

```bash
git config --list --global
```

## Local Git

### Git Repoistory 생성

1. 디렉토리 생성
    
    ```bash
    mkdir ~/Desktop/workspace/daily-note
    
    ```
    
2. 디렉토리로 이동
    
    ```bash
    cd ~/Desktop/workspace/daily-note
    
    ```
    
3. git 레포지토리 초기화 
    
    ```bash
    git init
    ```
    
4. 확인
    
    ```bash
    ~/Desktop/workspace/daily-note (master) $ ls -al
    total 8
    drwxr-xr-x 1 user 197121 0 Jan 29 20:54 ./
    drwxr-xr-x 1 user 197121 0 Jan 29 20:54 ../
    drwxr-xr-x 1 user 197121 0 Jan 29 20:54 .git/
    ```
    
    ```bash
    git status
    ```
    

### 파일 생성 및 최초 커밋

1. `daily-note.md` 파일 편집
    
    ```bash
    vi daily-note.md
    ```
    
    ```yaml
    # 2024년
    ## 2월
    ### 2024-02-01
    ```
    
    - 수정 후 `:wq`
2. git 상태 확인
    
    ```bash
    git status
    ```
    
3. 스테이지 올리기
    
    ```bash
    git add daily-note
    ```
    
4. git 상태 확인
    
    ```bash
    git status
    ```
    
5. git 커밋
    
    ```bash
    git commit -m "initial commit"
    ```
    
6. git 상태 확인
    
    ```bash
    git status
    ```
    

### Git commit 쌓기

<aside>
💡 여러분의 오늘 하루 일정을 한줄씩 넣어 commit을 쌓으세요.(10분)

</aside>

- 한줄씩 입력하고 `git add` & `git commit`
- [파일 생성 및 최초 커밋](https://www.notion.so/0fa5b7a100c54763a0508c655a2b112f?pvs=21) #1~#5 반복
- **commit 5개 이상 쌓기**

### Git 히스토리 확인

1. git 로그 확인
    
    ```bash
    git log
    ```
    
2. git diff
    
    ```bash
    git diff
    ```
    
3. git 로그 확인(2)
    
    ```bash
    git log --patch -2
    ```
    

### Git branch

1. 브랜치 확인
    
    ```bash
    git branch
    ```
    
2. 브랜치 생성
    
    ```bash
    git branch feature/a
    ```
    
3. 브랜치 이동
    
    ```bash
    git checkout feature/a
    ```
    
4. 파일 생성
    
    ```bash
    cat <<EOF > a.txt
    feature/a
    EOF
    ```
    
5. git 커밋
    
    ```bash
    git add a.txt
    git commit -m "add a.txt"
    ```
    
6. 기본 브랜치로 이동
    
    ```bash
    git checkout main
    ```
    

### Git 병합 및 충돌 해결

1. 브랜치 생성
    
    ```bash
    git branch feature/b
    ```
    
2. 브랜치 이동
    
    ```bash
    git checkout feature/b
    ```
    
3. `a.txt` 파일 생성
    
    ```bash
    cat <<EOF > a.txt
    feature/b
    EOF
    ```
    
4. git 커밋
    
    ```bash
    git add a.txt
    git commit -m "add a.txt"
    ```
    
5. `b.txt` 파일 생성
    
    ```bash
    cat <<EOF > b.txt
    This is feature/b
    EOF
    ```
    
6. git 커밋
    
    ```bash
    git add b.txt
    git commit -m "add b.txt"
    ```
    
7. 기본 브랜치로 이동
    
    ```bash
    git checkout main
    ```
    
8. `feature/a` 브랜치 병합
    
    ```bash
    git merge feature/a
    ```
    
9. `feature/b` 브랜치 병합
10. 충돌 해결
    
    ```
    <<<<<<< HEAD
    feature/b
    =======
    feature/A
    >>>>>>> <commit-hash>
    ```
    
    - `<<<<<<< HEAD` , `=======` , `>>>>>>> <commit-hash>` 제거 후, 내용 수정
11. git 커밋
    
    ```bash
    git add a.txt
    git commit -m "add b.txt"
    ```
    

### Git 되돌리기와 초기화

1. git n번째 commit sha 값 저장(예: 5번째)
    
    ```bash
    export sha=$(git log -n 6 --pretty=format:"%H" | sed -n '6p')
    ```
    
2. sha 값 확인
    
    ```bash
    echo $sha
    ```
    
3. git 되돌리기
    
    ```bash
    git revert $sha
    ```
    
4. 파일 수정 후 커밋
    
    ```bash
    vi daily-note.md
    git add daily-note.md
    git commit
    ```
    

### Git  초기화

1. git n번째 commit sha 값 저장(예: 1번째)
    
    ```bash
    export sha=$(git log -n 2 --pretty=format:"%H" | sed -n '2p')
    ```
    
2. sha 값 확인
    
    ```bash
    echo $sha
    ```
    
3. git 되돌리기
    
    ```bash
    git reset --hard $sha
    ```