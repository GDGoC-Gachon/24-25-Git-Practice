# 🌊 [LV300] 협업에서 발생하는 Git 문제 해결!

**시나리오:**
이제 프로젝트가 본격적으로 진행되면서 여러 팀원이 동시에 작업을 하다 보면, 다양한 충돌과 실수가 발생합니다. 우리는 이러한 상황에서 어떻게 문제를 해결하고, 효율적으로 협업할 수 있을지 배우게 됩니다!

## 🚤 1단계: Git Conflict 해결하기
팀원과 동시에 같은 파일을 수정하다가 Git Conflict가 발생했습니다.
이러한 충돌은 팀 프로젝트에서 가장 흔히 발생하는 문제 중 하나입니다. 이 문제를 어떻게 해결할 수 있을까요?

### 🚤 1.1 실습 환경 세팅
우선 lv300 실습을 위한 환경 세팅을 진행해보겠습니다. `lv300/<본인 이름>`의 형태로 본인 브랜치를 만들어 주세요.
```bash
git branch lv300/<본인 이름>
git switch lv300/<본인 이름>
```
### 🚤 1.2 Git Conflict 발생
(내용 작성)

### 🚤 1.3 Git Conflict 해결
(내용 작성)

<br><br>

## 🏝 2단계: 커밋 실수 해결하기
여러 파일을 수정하면서 각 파일에 대한 커밋 메시지를 개별적으로 작성해야 했지만, 실수로 여러 파일을 모두 같은 커밋 메시지로 작성해버렸습니다. 이 문제를 어떻게 해결할 수 있을까요?

### 🏝 2.1 직전 커밋 수정
방금 커밋한 메시지를 수정하고 싶다면, `git amend` 명령어를 사용하여 직전 커밋을 수정할 수 있습니다. 이때 수정된 내용은 새 커밋을 만들지 않고, 마지막 커밋을 덮어씁니다.
```bash
git commit --amend
```

- 본인의 브랜치에 `file1.txt`, `file2.txt` 파일을 생성 후 자유롭게 내용을 작성해주세요.
- 다음 명령어를 따라 두 파일 모두 커밋 후 푸시합니다.
```bash
git add .
git commit -m "file1 작업 완료"
git push origin lv300/<본인 이름>
```
- 작업 내용이 원격 저장소에 올라가긴 했지만, 우리는 file1과 file2, 두 파일을 작업하였으므로 커밋 메시지 내용을 바꿔보겠습니다.
- `amend`를 사용해 직전 커밋을 수정하고, `force`를 사용해 강제 푸시합니다.
```bash
git commit --amend -m "file1, file2 작업 완료"
git push --force origin lv300/<본인 이름>
```
<img width="404" alt="스크린샷 2024-10-03 오후 2 49 35" src="https://github.com/user-attachments/assets/8d6ed4f4-c498-4da0-b6b9-4ccfe6bc4501">


### 🏝 2.2 직전 커밋 취소
`git reset --soft` 명령어를 사용하여 특정 커밋을 취소할 수 있습니다.
이때 해당 커밋 이후의 변경사항은 스테이징 상태로 유지됩니다.
```bash
git reset --soft HEAD~1
```
- file1과 file2의 내용을 각각 커밋하려고 합니다.
- `reset --soft`를 사용해 커밋을 취소하고, `reset`으로 파일들을 스테이징 영역에서 제거합니다.
```bash
git reset --soft HEAD~1
git reset file1
git reset file2
```
- 이제 file1과 file2를 개별적으로 다시 커밋합니다.
```bash
git add file1.txt
git commit -m "file1 작업 완료"
git add file2.txt
git commit -m "file2 작업 완료"
git push --force origin lv300/<본인 이름>
```
<img width="358" alt="스크린샷 2024-10-03 오후 2 59 16" src="https://github.com/user-attachments/assets/890897ad-41ae-4088-bafe-fa4e9292f145">

<br><br>

## ⛴️ 3단계: Git Reset 실수 복구하기
실수로 `git reset` 명령어를 잘못 실행하여, 특정 커밋 이후의 작업물들이 사라졌습니다. 이 문제를 어떻게 해결할 수 있을까요?

### ⛴️ 3.1 Git reflog로 복구
다행히 Git은 모든 변경 사항을 기록하고 있기에 이를 복구할 수 있습니다. `git reflog` 명령어를 통해 커밋 기록을 확인하여 이를 해결할 수 있습니다.
```bash
git reflog
```
- 우선 본인의 브랜치에 이전에 생성했던 `file1.txt` 파일의 내용을 자유롭게 수정해주세요.
- 다음 명령어를 따라 두 파일 모두 커밋 후 푸시합니다.
```bash
git add file1.txt
git commit -m "file1 내용 수정"
git push origin lv300/<본인 이름>
```
<img width="333" alt="스크린샷 2024-10-08 오전 10 51 15" src="https://github.com/user-attachments/assets/991e43fb-cf4b-4669-ad0c-6f82aadf5130">

- 이제 실수 상황 재현을 위해 `git reset --hard` 명령어를 사용해 이전 커밋으로 되돌아갑니다.
- `file1.txt`에 대한 작업이 사라지게 되지만, 원격 저장소에는 여전히 해당 커밋이 남아 있습니다.
```bash
git reset --hard HEAD~1
```
- `git reflog` 명령어를 사용하여 이전 커밋의 기록을 확인하고, 사라진 커밋의 해시 값을 찾습니다.
```bash
git reflog
```
<img width="465" alt="스크린샷 2024-10-08 오전 10 58 04" src="https://github.com/user-attachments/assets/e8983d24-d032-491c-94b7-204dbe7dcb79">

- `git reset --hard` 명령어를 사용해 사라진 커밋으로 돌아갑니다. 이를 통해 `file2.txt`의 작업이 복구됩니다.
```bash
git reset --hard <복구할 커밋 해시>
```
<img width="299" alt="스크린샷 2024-10-08 오전 11 02 50" src="https://github.com/user-attachments/assets/bf17f43b-f5fc-4478-a98f-97300464e2f0">

- 로컬 저장소와 원격 저장소의 상태가 다르기 때문에, 강제로 푸시하여 복구된 내용을 원격 저장소에 반영합니다.
```bash
git push --force origin lv300/<본인 이름>
```
<img width="295" alt="스크린샷 2024-10-08 오전 11 04 05" src="https://github.com/user-attachments/assets/13914823-5654-4988-a114-a672491d1326">

<br><br>

## 🏖️ 4단계: Gitignore의 중요성
API 키나 비밀번호와 같은 중요한 정보를 실수로 깃허브에 올리면 어떻게 될까요? 이를 방지하기 위해 gitignore 파일을 사용하는 방법을 배워봅시다.

### 🏖️ 4.1 커밋의 무게
**1. 커밋의 무게란?**

커밋은 단순히 파일을 저장하는 것 이상의 작업입니다. 커밋은 영구적인 기록이며, 한번 커밋된 내용은 히스토리에서 삭제하거나 숨기는 것이 매우 어렵습니다. 특히 민감한 정보가 포함된 커밋이 원격 저장소로 푸시되면, 그 정보는 즉각적으로 깃허브에 올라가게 되고, 여러 사람에게 노출될 위험이 생깁니다.

**2. API 키가 깃허브에 올라가면?**

- **보안 침해:**
API 키나 비밀번호가 깃허브에 공개되면, 이를 이용해 제3자가 서비스에 접속하거나 악용할 수 있습니다. 이는 프로젝트의 보안뿐만 아니라 사용자의 데이터에도 큰 위협이 됩니다.

- **키를 재발급해야 하는 불편:**
노출된 키를 빠르게 폐기하고 새로운 키를 발급받아야 합니다. 이는 프로젝트의 진행에 큰 차질을 빚게 됩니다.

- **커밋 삭제의 어려움:**
커밋은 한번 푸시되면 히스토리에서 완전히 제거하기가 어렵습니다. `git rebase`나 `git filter-branch` 명령어를 사용해 커밋을 제거할 수 있지만, 원격 저장소에 이미 푸시된 내용을 다른 사람들도 가지고 있을 수 있기 때문에, 이 작업은 매우 복잡하고 많은 시간 또한 소모됩니다.

### 🏖️ 4.2 Gitignore 설정
**1. .gitignore 파일 생성 및 설정**

`.gitignore` 파일을 통해 특정 파일이나 폴더를 깃이 추적하지 않도록 설정할 수 있습니다. 예시로 `node_modules/`, `.env` 파일 등을 `.gitignore`에 추가합니다.

<img width="247" alt="스크린샷 2024-09-23 오후 10 19 54" src="https://github.com/user-attachments/assets/35c0c1a2-c57f-4422-88f3-74693bc45407">

**2. .gitignore 실습**
- 본인 브랜치에 `file3.txt` 파일과 `.gitignore` 파일을 생성합니다.
- `.gitignore` 파일 안에 file3.txt라는 내용을 추가합니다.
<img width="199" alt="스크린샷 2024-10-08 오후 1 19 22" src="https://github.com/user-attachments/assets/b5d236b1-4e5e-41fb-9e70-83200361bd54">

- 다음 명령어를 따라 커밋과 푸시를 진행합니다.
```bash
git add .
git commit -m "gitignore 설정"
git push origin lv300/<본인 이름>
```
- 다음과 같이 원격 저장소에는 `file3.txt` 파일이 추적되지 않는 것을 확인할 수 있습니다.
<img width="235" alt="스크린샷 2024-10-08 오후 1 21 40" src="https://github.com/user-attachments/assets/59200368-aec2-4536-8d55-4ed82eadfdff">

<br><br>

---
**🎉 축하합니다! 이제 여러 문제 상황을 해결할 수 있는 방법을 익혔습니다!**

오늘 배운 내용을 바탕으로, 앞으로 협업 과정에서 마주하는 문제들을 다양한 방법으로 해결해 보세요!
