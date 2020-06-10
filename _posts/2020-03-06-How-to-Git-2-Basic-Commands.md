---
title: "How to Git (2) - Basic Commands"
categories: 
  - dev
  - How to git
last_modified_at: 2020-06-09T00:00:00+09:00
toc: true
author_profile: true
tag: 
  - git
---

기본 개념에 이어 기초적인 Git 동작을 위한 Git Commands를 정리하였다. 예시는 모두 Git Bash 기준이다.

# Git Commands - Basic

## How to make Repository

### Init

```sh
git init
```

> 현재 폴더를 Git 리파지토리로 만드는 작업

이 명령어는 현재 폴더가 Git Repository가 아닐 때, Local Repository를 만드는 작업을 한다. 이 작업을 수행하면 .git 디렉터리가 생성된다. 이 디렉터리는 이 폴더와 이하의 파일들이 Git Repository는 것을 의마한다.
이 .git 디렉터리는 숨김폴더로 지정되어있는데, 내부를 들여다보면 현재 HEAD, index 등의 정보가 정리된 파일이 있는 것을 볼 수 있다.

이 경우에는 Remote Repository를 지정하지 않은 상태이므로 ```git remote add``` 명령어를 통해 Remote Repository를 지정해주면 push할 수 있는 상태가 된다.

### Clone

```sh
git clone [Remote Repository URL]
```

> Remote Repository를 내려받아 Local Repository로 만들기

이 명령어는 이미 생성된 Remote Repository의 내용을 받아 Local Repository로 복사해서 작업하고 싶을 때 사용한다.
만약 특정 브랜치를 내려받고 싶다면 **-b** 옵션을 사용해서 브랜치를 선택하여 내려받을 수 있다.

## How to make Branches

### Branch

```sh
git branch [Branch Name]
```

> 현재 Repository에서 새 브랜치를 만들고 싶을 때

`git init`으로 Repository를 생성하게 되면 master브랜치가 기본으로 만들어져 있다. git bash에도 *(master)* 라고 되어있을 것이다. 만약 `git branch dev`로 개발 브랜치를 생성하게 되면 아직 나의 working tree는 master브랜치에 있는 상태로 dev 브랜치가 생성된다.

### Checkout

```sh
git checkout [Branch Name]
```

> 다른 브랜치로 이동하기

새로 생성한 브랜치로 이동하고 싶거나 작업 중 브랜치를 변경하고 싶을 때 이 명령어를 사용한다. `git checkout dev` 명령어를 입력하면 git bash에도 *(dev)* 로 바뀐 것이 보일 것이다.

## Commit Your File

이제 파일을 하나 수정했다고 가정해보자. 즉, Working Tree에 변화가 있는 상태를 만든다. (기존에 Tracking되는 파일을 수정했다거나, 새로운 파일 *—Untracking 상태의—* 을 만들었다던지)

### Status

```sh
git status
```

> 현재 Working Tree의 상태를 보기

이 명령어를 사용하면 현재 Working Tree의 상태를 볼 수 있다. 어떤 파일이 modified상태인지 staged 상태인지 등을 볼 수 있다. 이제 다음으로 Commit하고 싶은 파일을 추가해보자.

### Add

```sh
git add [File/Folder]
```

> 파일이나 폴더를 Index에 추가하기. Staged 상태로 만들기.

Commit하고 싶은 파일을 Staged Area에 추가하는 작업이다. 만약 추가했던 파일을 다시 unstaged 상태로 만들고 싶으면 `git reset [File/Folder]`로 제외시킬 수 있다.

add후 `git status`를 수행해보면 staged된 파일들이 초록색으로 표시됨을 볼 수 있다.

### Commit

```sh
git commit
```

> 커밋 수행하기

위 명령어를 입력하면 이전에 보여지던 git bash 로그들이 사라지고 **Vim** 에디터 화면이 뜬다.(Default로 git을 설치했을 경우) 이 화면은 Commit 메시지를 편집하기 위한 화면이다.

Vim은 Linux OS에서 주로 사용하는 텍스트 에디터이다. 이 에디터에는 세가지 모드가 있는데 Insert Mode(텍스트 수정), Normal Mode(모드 변경), EX Mode(명령 모드)가 있다. 처음 보이는 화면은 Normal Mode로 열린 상태이다. 이 때 키보드로 **i** 키를 입력하면 Insert Mode가 된다. 간략한 Vim명령어는 아래 표를 참고하면 된다.

| 명령어 | 설명                |
|:----:|--------------------|
|   i  | Insert Mode(Edit)  |
|  ESC | Normal Mode        |
|   :  | EX Mode            |
|  :w  | Write(Save)        |
|  :q  | Quit               |
| :wq  | Write and Quit     |

Insert Mode 상태에서 Commit 메시지를 입력한 후 **ESC** 키를 눌러 Normal Mode로 빠져나온다. 이제 저장하고 에디터를 종료하기 위해서 **:wq** 라고 입력하면 가장 아래 줄에 입력이 되는 것을 볼 수 있다. 명령어를 입력하고 **Enter** 를 입력하면 메시지가 저장이 되며 Commit이 수행된다.

만약 Vim을 사용하기 번거롭다면 간단하게 Commit을 할 수 있는 명령어도 있다!

```sh
git commit -m "Commit Message Here"
```

## View Your Commits

### Log

```sh
git log
```

> 현재 Repository의 Commit History 보기

방금했던 Commit의 내용이나 이전의 Commit 내용들을 보고 싶은 경우 사용한다. Commit번호와 Author, Date, Message등이 출력되고 Remote/Local Repository의 어떤 브랜치가 어떤 Commit을 보고 있는지도 표시된다.


이제 Remote Repository에 Push하기 전 Remote Repository가 다른 사람에 의해 업데이트 되지는 않았는 지 체크해보도록 하자.

## Get Remote Repository Status

### Fetch

```sh
git fetch
```

> Remote Repository의 변경사항을 가져오나 Local Repository를 변경시키지 않음

### Pull

```sh
git pull
```

> Remote Repository의 가져와서 Local Repository에 반영함

만약 Local에서 새로 만든 브랜치가 있다면 Remote에는 이 브랜치가 없으므로 아무것도 pull되지 않는다.

## Merge Branches

### merge

```sh
git merge [Branch Name]
```

> 다른 브랜치를 현재 브랜치에 합치기

먼저 합침을 당할(?) *—Merge Into—* 될 브랜치로 `git checkout`을 통해 이동한다. 이후 합치고 싶은 브랜치 *—Merge From—* 에 대해 `git merge`를 수행한다. 보통은 feature 브랜치가 dev 브랜치로 merge된다거나, dev 브랜치가 release 또는 master 브랜치로 merge될 것이다.

Auto Merge가 될 수도 있지만, 같은 파일의 같은 라인을 수정한 경우에는 Conflict가 발생할 수도 있다. 이는 다음 포스트에서 설명하기로 한다.

Merge후 feature브랜치 등을 사용하지 않게된다면 `git branch -d [Branch Name]`으로 브랜치를 지울 수 있다.

## Update Remote Repository

### Push

```sh
git push
```

> Local Repository의 내용을 Remote Repository에 반영하기

Merge나 Commit등으로 Remote의 Index보다 앞서고, Conflict가 없는 경우 성공적으로 Remote에 Push할 수 있다. GitHub등에 접속해서 Remote의 내용을 보면 업데이트가 잘 되었다는 것을 볼 수 있을 것이다.

다음 포스트에서는 특정 상황이 발생했을 때 해결할 수 있는 Git Command를 살펴보기로 한다.
