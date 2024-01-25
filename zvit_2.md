## Національний технічний університет України<br>“Київський політехнічний інститут ім. Ігоря Сікорського”

  

## Факультет прикладної математики<br>Кафедра системного програмування і спеціалізованих комп’ютерних систем

  
  

# Лабораторна робота №2<br>"Розширена робота з git"

  

## КВ-12 Дубіковська Дана Дарина

  

## Хід виконання роботи

### 1. Зклонувати репозиторій для ЛР2 використавши локальний репозиторій від ЛР1 в якості "віддаленого".

Клонуємо код першої нашої лабораторної командою `git clone file:////home/dana2/lababa1/dubik`

```bash
dana2@PC:~/lab2$ git clone file:////home/dana2/lababa1/dubik
Cloning into 'dubik'...
remote: Enumerating objects: 22, done.
remote: Counting objects: 100% (22/22), done.
remote: Compressing objects: 100% (14/14), done.
remote: Total 22 (delta 1), reused 0 (delta 0)
Receiving objects: 100% (22/22), done.
Resolving deltas: 100% (1/1), done.
```
### 2. Робота з ремоутами.
#### 2.1 Додати новий ремоут використавши URI на інтернет-джерело вашого репозиторію.

Для цього використаємо команду `git remote -v`, що б зі списку доступних отримати URI нам потрібного. Далі командою `git remote add upstream` додаємо наш ремоут

```bash
dana2@PC:~/lab2/dubik$ git remote -v
origin  file:////home/dana2/lababa1/dubik (fetch)
origin  file:////home/dana2/lababa1/dubik (push)
dana2@PC:~/lab2/dubik$ git remote add upstream https://github.com/danonchik2/dubik.git
dana2@PC:~/lab2/dubik$ git remote -v
origin  file:////home/dana2/lababa1/dubik (fetch)
origin  file:////home/dana2/lababa1/dubik (push)
upstream        https://github.com/danonchik2/dubik.git (fetch)
upstream        https://github.com/danonchik2/dubik.git (push)
```

#### 2.2 Показати список віддалених гілок, так щоби було видно гілки з різних ремоутів.

Виконуємо команду `git fetch upstream`, що б підтягти зміни, та використовуємо `git branch -a` що б побачити гілки з усіх ремоутів
```bash
dana2@PC:~/lab2/dubik$ git fetch upstream
remote: Enumerating objects: 7, done.
remote: Counting objects: 100% (7/7), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 6 (delta 0), reused 6 (delta 0), pack-reused 0
Unpacking objects: 100% (6/6), 2.42 KiB | 353.00 KiB/s, done.
From https://github.com/danonchik2/dubik
 * [new branch]      main       -> upstream/main
dana2@PC:~/lab2/dubik$
dana2@PC:~/lab2/dubik$  git branch -a
* main
  remotes/origin/HEAD -> origin/main
  remotes/origin/main
  remotes/origin/my-local-branch-1
  remotes/origin/my-local-branch-2
  remotes/upstream/main
```
#### 2.3 Створити нову гілку lab2-branch, додати в нього кілька комітів.

Створимо нову гілку командою `git checkout -b lab2-branch`, та створивши кілька файлів, командою `git commit` зробимо три коміти

```bash
dana2@PC:~/lab2/dubik$ git checkout -b lab2-branch
Switched to a new branch 'lab2-branch'
dana2@PC:~/lab2/dubik$ git branch -a
* lab2-branch
  main
  remotes/origin/HEAD -> origin/main
  remotes/origin/main
  remotes/origin/my-local-branch-1
  remotes/origin/my-local-branch-2
  remotes/upstream/main
dana2@PC:~/lab2/dubik$ git status
On branch lab2-branch
nothing to commit, working tree clean
dana2@PC:~/lab2/dubik$ vim new1.txt
dana2@PC:~/lab2/dubik$ git add new1.txt
dana2@PC:~/lab2/dubik$ git commit -am "added new1.txt"
[lab2-branch b0deb93] added new1.txt
 1 file changed, 1 insertion(+)
 create mode 100644 new1.txt
dana2@PC:~/lab2/dubik$ vim new2.txt
dana2@PC:~/lab2/dubik$ git add new2.txt
dana2@PC:~/lab2/dubik$ git commit -m "added neww.txt"
[lab2-branch 39e6aed] added neww.txt
 1 file changed, 1 insertion(+)
 create mode 100644 new2.txt
dana2@PC:~/lab2/dubik$ vim new3.txt
dana2@PC:~/lab2/dubik$ git add new3.txt
dana2@PC:~/lab2/dubik$ git commit -m "added new3.txt"
[lab2-branch ff97a85] added new3.txt
 1 file changed, 1 insertion(+)
 create mode 100644 new3.txt
```

#### 2.4 Пушнути гілку lab2-branch на ремоут, створений з ЛР1 без зв'язування локальної гілки з віддаленою.

Що б не звязувати локальну гілку з віддаленою, потрібно явно задати параметри рімоута та гілки, і не використовувати параметр `-u` в команді `git push origin lab2-branch`

```bash
dana2@PC:~/lab2/dubik$ git push origin lab2-branch
Enumerating objects: 10, done.
Counting objects: 100% (10/10), done.
Delta compression using up to 4 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (9/9), 724 bytes | 362.00 KiB/s, done.
Total 9 (delta 2), reused 0 (delta 0)
To file:////home/dana2/lababa1/dubik
 * [new branch]      lab2-branch -> lab2-branch
```
#### 2.5 Додати до гілки ще коміт

Додаємо коміт зміною значення у файлі.

```bash
dana2@PC:~/lab2/dubik$ vim new1.txt
dana2@PC:~/lab2/dubik$ git status -uno
On branch lab2-branch
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   new1.txt

no changes added to commit (use "git add" and/or "git commit -a")
dana2@PC:~/lab2/dubik$ git add new1.txt
dana2@PC:~/lab2/dubik$ git status -uno
On branch lab2-branch
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   new1.txt

Untracked files not listed (use -u option to show untracked files)
dana2@PC:~/lab2/dubik$ git commit -m "modified new1.txt"
[lab2-branch 5d2694b] modified new1.txt
 1 file changed, 1 insertion(+), 1 deletion(-)
```

#### 2.6 Пушнути зміни гілки на ремоут, створений з ЛР1, цього разу зв'язавши гілки.

Тепер зв'яжемо локальну гілку з ремоутною командою `git push -u origin lab2-branch`

```bash
dana2@PC:~/lab2/dubik$ git push -u origin lab2-branch
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 259 bytes | 259.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0)
To file:////home/dana2/lababa1/dubik
   ff97a85..5d2694b  lab2-branch -> lab2-branch
Branch 'lab2-branch' set up to track remote branch 'lab2-branch' from 'origin'.
dana2@PC:~/lab2/dubik$ git push
Everything up-to-date
```

Як бачимо, після команди `git push` отримуємо відповідь `Everything up-to-date`

#### 2.7 Додамо ще один коміт

```bash
dana2@PC:~/lab2/dubik$ vim new2.txt
dana2@PC:~/lab2/dubik$ git add new2.txt
dana2@PC:~/lab2/dubik$ git status -uno
On branch lab2-branch
Your branch is up to date with 'origin/lab2-branch'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   new2.txt

Untracked files not listed (use -u option to show untracked files)
dana2@PC:~/lab2/dubik$ git commit -m "modified new2.txt"
[lab2-branch 9f91b79] modified new2.txt
 1 file changed, 1 insertion(+), 1 deletion(-)
```

#### 2.8 Перевіряємо чи запрацює git push

```bash
dana2@PC:~/lab2/dubik$ git push
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 262 bytes | 262.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0)
To file:////home/dana2/lababa1/dubik
   5d2694b..9f91b79  lab2-branch -> lab2-branch
```

#### 2.9 Перевіряємо наявність нової гілки у підключеному репозиторії

```bash
dana2@PC:~/lababa1/dubik$ git branch -a
  lab2-branch
* main
  my-local-branch-1
  my-local-branch-2
  remotes/origin/HEAD -> origin/main
  remotes/origin/main
```

### 3. Змерджити гілку, що була створена при виконанні ЛР1, в поточну гілку lab2-branch

Командами `git merge origin/my-local-branch-2` та `git log --pretty=oneline --graph` отримаємо інформацію про розходження гілок

```bash
dana2@PC:~/lab2/dubik$ git branch -a
* lab2-branch
  main
  remotes/origin/HEAD -> origin/main
  remotes/origin/lab2-branch
  remotes/origin/main
  remotes/origin/my-local-branch-1
  remotes/origin/my-local-branch-2
  remotes/upstream/main
dana2@PC:~/lab2/dubik$ git merge origin/my-local-branch-2
Already up to date.
dana2@PC:~/lab2/dubik$ ls
main.c  new1.txt  new2.txt  new3.txt  old.txt
dana2@PC:~/lab2/dubik$ git log --pretty=oneline --graph
* 9f91b796446bba50ba5b1132764f47e2a5aa629b (HEAD -> lab2-branch, origin/lab2-branch) modified new2.txt
* 5d2694b4efa98df2052e83eee4bcf7d9de858be6 modified new1.txt
* ff97a85e254e5070565db59e8ef57b029cb3a176 added new3.txt
* 39e6aed0a7fbe0b2fe82c3809fb8ee7c6dd7384c added neww.txt
* b0deb93085aa65d56613e8ab38b4a3eeb7656349 added new1.txt
* d615f0379010aa45c1ae5588dcce89038dad9f19 (origin/main, origin/HEAD, main) different name for a commit
* 4a038c6305a574aeec7403f76a3cfad119066d88 (origin/my-local-branch-2) stable
* 3424717c6a0e2d28afbd475374cbd8259d84b766 new file 2 back 2
* 2da016075bc5632848ec76c4a0015c0ac5d513be add main.c
* ad80ab85caa0c5c158a5ec88ade48ebe1bcf2a90 dl 1.txt
* 4de4d9433258abfc727647d49d0907ef5db6ed60 rm 1
* ad0dce95b8f3713129e1106e1bd9c7a2a219e02d cam
* 64f4f20aefea34875eb2eecb11879731d53aba0f init
```

### 4. Перенесення комітів
#### 4.1 Створити ще одну гілку від master-a lab2-branch-2, додати в неї три коміти. 

```bash
dana2@PC:~/lab2/dubik$ git checkout -b lab2-branch-2
Switched to a new branch 'lab2-branch-2'
dana2@PC:~/lab2/dubik$ ls
main.c  new1.txt  new2.txt  new3.txt  old.txt
dana2@PC:~/lab2/dubik$ vim new1.txt
dana2@PC:~/lab2/dubik$ git add new1.txt
dana2@PC:~/lab2/dubik$ git commit -m "test commit 1"
[lab2-branch-2 2f9f8e6] test commit 1
 1 file changed, 1 insertion(+), 1 deletion(-)
dana2@PC:~/lab2/dubik$ vim new2.txt
dana2@PC:~/lab2/dubik$ git add new2.txt
dana2@PC:~/lab2/dubik$ git commit -m "test commit 2"
[lab2-branch-2 adf7bb6] test commit 2
 1 file changed, 1 insertion(+), 1 deletion(-)
dana2@PC:~/lab2/dubik$ vim new3.txt
dana2@PC:~/lab2/dubik$ git add new3.txt
dana2@PC:~/lab2/dubik$ git commit -m "test commit 3"
[lab2-branch-2 2aa795f] test commit 3
 1 file changed, 1 insertion(+), 1 deletion(-)
```
#### 4.2 Перенести з гілки lab2-branch-2 середній з трьох нових комітів в гілку lab2-branch.

Шукаємо серед створених комітів середній, копіюємо його токен та чері-пікаєм його у наш бренч

```bash
dana2@PC:~/lab2/dubik$ git log
commit 2aa795fe4340cd0f4183e03e5e2fd769a86b919c (HEAD -> lab2-branch-2)
Author: daruna <danadarinad@gmail.com>
Date:   Wed Jan 24 21:33:48 2024 +0200

    test commit 3

commit adf7bb6ae662ac4f6e383d841363871ff3f6da86
Author: daruna <danadarinad@gmail.com>
Date:   Wed Jan 24 21:33:11 2024 +0200

    test commit 2

commit 2f9f8e6164fa2e23f5ca988170bb5c2ccde168ea
Author: daruna <danadarinad@gmail.com>
Date:   Wed Jan 24 21:32:34 2024 +0200

    test commit 1

commit 9f91b796446bba50ba5b1132764f47e2a5aa629b (origin/lab2-branch, lab2-branch)
Author: daruna <danadarinad@gmail.com>
Date:   Wed Jan 24 21:07:24 2024 +0200

    modified new2.txt

commit 5d2694b4efa98df2052e83eee4bcf7d9de858be6
Author: daruna <danadarinad@gmail.com>
Date:   Wed Jan 24 21:01:23 2024 +0200

    modified new1.txt

commit ff97a85e254e5070565db59e8ef57b029cb3a176
Author: daruna <danadarinad@gmail.com>
Date:   Wed Jan 24 19:22:35 2024 +0200

    added new3.txt

commit 39e6aed0a7fbe0b2fe82c3809fb8ee7c6dd7384c
Author: daruna <danadarinad@gmail.com>
Date:   Wed Jan 24 19:21:47 2024 +0200

dana2@PC:~/lab2/dubik$ git checkout lab2-branch
Switched to branch 'lab2-branch'
Your branch is up to date with 'origin/lab2-branch'.
dana2@PC:~/lab2/dubik$ git cherry-pick adf7bb6ae662ac4f6e383d841363871ff3f6da86
[lab2-branch 6ea74ea] test commit 2
 Date: Wed Jan 24 21:33:11 2024 +0200
 1 file changed, 1 insertion(+), 1 deletion(-)
dana2@PC:~/lab2/dubik$ git log
commit 6ea74ea7f95ff69cbbdeac81c9ff25c61b3ff073 (HEAD -> lab2-branch)
Author: daruna <danadarinad@gmail.com>
Date:   Wed Jan 24 21:33:11 2024 +0200

    test commit 2

commit 9f91b796446bba50ba5b1132764f47e2a5aa629b (origin/lab2-branch)
Author: daruna <danadarinad@gmail.com>
Date:   Wed Jan 24 21:07:24 2024 +0200

    modified new2.txt

commit 5d2694b4efa98df2052e83eee4bcf7d9de858be6
Author: daruna <danadarinad@gmail.com>
Date:   Wed Jan 24 21:01:23 2024 +0200

    modified new1.txt

commit ff97a85e254e5070565db59e8ef57b029cb3a176
Author: daruna <danadarinad@gmail.com>
Date:   Wed Jan 24 19:22:35 2024 +0200

    added new3.txt

commit 39e6aed0a7fbe0b2fe82c3809fb8ee7c6dd7384c
Author: daruna <danadarinad@gmail.com>
Date:   Wed Jan 24 19:21:47 2024 +0200

    added neww.txt

commit b0deb93085aa65d56613e8ab38b4a3eeb7656349
Author: daruna <danadarinad@gmail.com>
Date:   Wed Jan 24 19:20:33 2024 +0200

    added new1.txt

commit d615f0379010aa45c1ae5588dcce89038dad9f19 (origin/main, origin/HEAD, main)
Author: daruna <danadarinad@gmail.com>
Date:   Wed Jan 24 14:04:34 2024 +0200
```

### 5. Визначити останнього спільного предка між двома будь-якими гілками.

Використаємо команду `git merge-base origin/lab2-branch origin/my-local-branch-2`

```bash
dana2@PC:~/lab2/dubik$  git merge-base origin/lab2-branch origin/my-local-branch-2
4a038c6305a574aeec7403f76a3cfad119066d88
```
### 6. Робота з ничкою. 
#### 6.1 Зробити трохи unstaged змін. 
```bash
dana2@PC:~/lab2/dubik$ git status
On branch lab2-branch
Your branch is ahead of 'origin/lab2-branch' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
dana2@PC:~/lab2/dubik$ vim new1.txt
dana2@PC:~/lab2/dubik$ vim new2.txt
dana2@PC:~/lab2/dubik$ git status
On branch lab2-branch
Your branch is ahead of 'origin/lab2-branch' by 1 commit.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   new1.txt
        modified:   new2.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
#### 6.2 Зберегти до нички. 

Застосуємо команду `git stash`

```bash
dana2@PC:~/lab2/dubik$ git stash
Saved working directory and index state WIP on lab2-branch: 6ea74ea test commit 2
dana2@PC:~/lab2/dubik$ git status
On branch lab2-branch
Your branch is ahead of 'origin/lab2-branch' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```
#### 6.3 Зробити ще трохи unstaged змін. 

```bash
dana2@PC:~/lab2/dubik$ vim new3.txt
dana2@PC:~/lab2/dubik$ git status
On branch lab2-branch
Your branch is ahead of 'origin/lab2-branch' by 1 commit.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   new3.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
#### 6.4 Зберегти до нички. 

Застосуємо команду `git stash`

```bash
dana2@PC:~/lab2/dubik$ git stash
Saved working directory and index state WIP on lab2-branch: 6ea74ea test commit 2
dana2@PC:~/lab2/dubik$ git status
On branch lab2-branch
Your branch is ahead of 'origin/lab2-branch' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```
#### 6.5 Дістати з нички перші збережені зміни, ті що збереглися на кроці (6.2)

Застосуємо команду `git stash list` що б перевірити збережені стани, та командою 
` git stash apply stash@{1}` застосовуємо перший збережений стан

```bash
dana2@PC:~/lab2/dubik$ git stash list
stash@{0}: WIP on lab2-branch: 6ea74ea test commit 2
stash@{1}: WIP on lab2-branch: 6ea74ea test commit 2
dana2@PC:~/lab2/dubik$ git stash apply stash@{1}
On branch lab2-branch
Your branch is ahead of 'origin/lab2-branch' by 1 commit.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   new1.txt
        modified:   new2.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
### 7. Робота з файлом .gitignore.
#### 7.1 Створити кілька файлів з якимось унікальним розширенням. 
```bash
dana2@PC:~/lab2/dubik$ vim test1.kvfpm
dana2@PC:~/lab2/dubik$ vim test2.kvfpm
dana2@PC:~/lab2/dubik$ vim test3.txt
dana2@PC:~/lab2/dubik$ git status
On branch lab2-branch
Your branch is ahead of 'origin/lab2-branch' by 1 commit.
  (use "git push" to publish your local commits)

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test1.kvfpm
        test2.kvfpm
        test3.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
#### 7.2 Додати шаблон для цих файлів в ігнор. 

Демонструю створення `.gitignore`
```bash
dana2@PC:~/lab2/dubik$ vim .gitignore
```
![[Pasted image 20240124233250.png]]
#### 7.3 Перевірити статус -- файли повинні зникнути. 

```bash
dana2@PC:~/lab2/dubik$ git status
On branch lab2-branch
Your branch is ahead of 'origin/lab2-branch' by 1 commit.
  (use "git push" to publish your local commits)

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore
        test3.txt
```
#### 7.4 Перевірити статус включно з ігнором. 
```bash
dana2@PC:~/lab2/dubik$ git status --ignored
On branch lab2-branch
Your branch is ahead of 'origin/lab2-branch' by 1 commit.
  (use "git push" to publish your local commits)

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore
        test3.txt

Ignored files:
  (use "git add -f <file>..." to include in what will be committed)
        test1.kvfpm
        test2.kvfpm
```
#### 7.5 Почистити всі untracked файли з репозиторію, включно з ігнорованими.

Використаємо команду `git clean -fdx`

```bash
dana2@PC:~/lab2/dubik$ git clean -fdx
Removing .gitignore
Removing test1.kvfpm
Removing test2.kvfpm
Removing test3.txt
dana2@PC:~/lab2/dubik$ git status
On branch lab2-branch
Your branch is ahead of 'origin/lab2-branch' by 1 commit.
  (use "git push" to publish your local commits)
  
nothing to commit, working tree clean
```
### 8. Робота з reflog. 
#### 8.1 Переглянути лог станів гілок. 

Використаємо команду `git reflog`

```bash
dana2@PC:~/lab2/dubik$ git reflog
d615f03 (HEAD -> main, origin/main, origin/HEAD) HEAD@{0}: checkout: moving from lab2-branch to main
6ea74ea HEAD@{1}: reset: moving to HEAD
6ea74ea HEAD@{2}: reset: moving to HEAD
6ea74ea HEAD@{3}: cherry-pick: test commit 2
9f91b79 HEAD@{4}: checkout: moving from lab2-branch-2 to lab2-branch
2aa795f (lab2-branch-2) HEAD@{5}: commit: test commit 3
adf7bb6 HEAD@{6}: commit: test commit 2
2f9f8e6 HEAD@{7}: commit: test commit 1
9f91b79 HEAD@{8}: checkout: moving from lab2-branch to lab2-branch-2
9f91b79 HEAD@{9}: commit: modified new2.txt
5d2694b HEAD@{10}: commit: modified new1.txt
ff97a85 HEAD@{11}: commit: added new3.txt
39e6aed HEAD@{12}: commit: added neww.txt
b0deb93 HEAD@{13}: commit: added new1.txt
d615f03 (HEAD -> main, origin/main, origin/HEAD) HEAD@{14}: checkout: moving from main to lab2-branch
d615f03 (HEAD -> main, origin/main, origin/HEAD) HEAD@{15}: clone: from file:////home/dana2/lababa1/dubik
```

#### 8.2 Створити нову гілку на будь-який стан зі списку та переключитися на цю гілку

Взявши код стану з попереднього списку, використаємо команду `git branch lab2-resurrected 6ea74ea`, та перейдемо на неї командою `git checkout lab2-resurrected`

```bash
dana2@PC:~/lab2/dubik$ git branch lab2-resurrected 6ea74ea
dana2@PC:~/lab2/dubik$ git checkout lab2-resurrected
Switched to branch 'lab2-resurrected'
dana2@PC:~/lab2/dubik$ git log --pretty=oneline --graph -n 15
* 6ea74ea7f95ff69cbbdeac81c9ff25c61b3ff073 (HEAD -> lab2-resurrected) test commit 2
* 9f91b796446bba50ba5b1132764f47e2a5aa629b modified new2.txt
* 5d2694b4efa98df2052e83eee4bcf7d9de858be6 modified new1.txt
* ff97a85e254e5070565db59e8ef57b029cb3a176 added new3.txt
* 39e6aed0a7fbe0b2fe82c3809fb8ee7c6dd7384c added neww.txt
* b0deb93085aa65d56613e8ab38b4a3eeb7656349 added new1.txt
* d615f0379010aa45c1ae5588dcce89038dad9f19 (origin/main, origin/HEAD, main) different name for a commit
* 4a038c6305a574aeec7403f76a3cfad119066d88 (origin/my-local-branch-2) stable
* 3424717c6a0e2d28afbd475374cbd8259d84b766 new file 2 back 2
* 2da016075bc5632848ec76c4a0015c0ac5d513be add main.c
* ad80ab85caa0c5c158a5ec88ade48ebe1bcf2a90 dl 1.txt
* 4de4d9433258abfc727647d49d0907ef5db6ed60 rm 1
* ad0dce95b8f3713129e1106e1bd9c7a2a219e02d cam
* 64f4f20aefea34875eb2eecb11879731d53aba0f init
```
