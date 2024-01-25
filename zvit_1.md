## Національний технічний університет України<br>“Київський політехнічний інститут ім. Ігоря Сікорського”

  

## Факультет прикладної математики<br>Кафедра системного програмування і спеціалізованих комп’ютерних систем

  
  

# Лабораторна робота №1<br>"Базова робота з git"

  

## КВ-12 Дубіковська Дана Дарина

  

## Хід виконання роботи

  

### 1. Зклонувати будь-який невеликий проєкт open-source з github

Чисто для прикладу використаємо якийсь більший open-source проект, щоб побачити різницю у розмірі
#### 1.1 Виконуємо команду, `git clone https://github.com/refinedev/refine.git

```bash
dana2@PC:~/lababa1$  git clone https://github.com/refinedev/refine.git
Cloning into 'refine'...
remote: Enumerating objects: 829975, done.
remote: Counting objects: 100% (42368/42368), done.
remote: Compressing objects: 100% (7390/7390), done.
Receiving objects: 100% (829975/829975), 1.72 GiB | 1.72 MiB/s, done.
remote: Total 829975 (delta 23568), reused 42233 (delta 23485), pack-reused 787607
Resolving deltas: 100% (534749/534749), done.
Updating files: 100% (10825/10825), done.
```

Тепер зклонуємо один бренч з проекту у папку "tutorial-branch" командою: `git clone git clone https://github.com/refinedev/refine.git--depth=1 --single-branch -b docs/new-tutorial tutorial-branch

```bash
dana2@PC:~/lababa1$ git clone https://github.com/refinedev/refine.git --depth=1 --single-branch -b docs/new-tutorial tutorial-branch
Cloning into 'tutorial-branch'...
remote: Enumerating objects: 11781, done.
remote: Counting objects: 100% (11781/11781), done.
remote: Compressing objects: 100% (7627/7627), done.
remote: Total 11781 (delta 3784), reused 7975 (delta 2745), pack-reused 0
Receiving objects: 100% (11781/11781), 25.67 MiB | 1.41 MiB/s, done.
Resolving deltas: 100% (3784/3784), done.
Updating files: 100% (10947/10947), done.
```

#### 1.2 Порівнюємо розміри командою `du -sh ./*/.git`

```bash
dana2@PC:~/lababa1$ du -sh ./*/.git
1.8G    ./refine/.git
28M     ./tutorial-branch/.git
```
### 2. Зробити не менше трьох локальних комітів

Використаємо якийсь особистий локальний репозиторій

Виконаємо зміни у файлі та створимо новий, після чого застосуємо команду `git status`

```bash
dana2@PC:~/lababa1/dubik$ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   main.c

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        new.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Як бачимо, наш новий файл не відслідковується

Скористаємося командою `git status -uno`

```bash
dana2@PC:~/lababa1/dubik$ git status -uno
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   main.c

no changes added to commit (use "git add" and/or "git commit -a")
```

Файл main.c змінений, але не доданий у коміт
#### 2.1. Додавання файлів до індексу:

Скористаємось командою `git commit -am "some changes to main.c"`

```bash
dana2@PC:~/lababa1/dubik$ git commit -am "some changes to main.c"
[main ad91b92] some changes to main.c
 1 file changed, 1 insertion(+)
```

Як бачимо, до коміту додало тільки змінений нами файл, що уже був проіндексований

```bash
dana2@PC:~/lababa1/dubik$ git status
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        new.txt

nothing added to commit but untracked files present (use "git add" to track)
```

Файл  new.txt так і не доданий, нам підказують як його додати (`nothing added to commit but untracked files present (use "git add" to track)`)

```bash
dana2@PC:~/lababa1/dubik$ git add new.txt
dana2@PC:~/lababa1/dubik$ git status
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   new.txt

dana2@PC:~/lababa1/dubik$ git commit -am "added new file"
[main 468d1b6] added new file
 1 file changed, 1 insertion(+)
 create mode 100644 new.txt
```
#### 2.2. Вказання різних повідомлень коміту:

Створимо ще один коміт з іншою назвою

```bash
dana2@PC:~/lababa1/dubik$ git commit -m "different name for a commit"
[main d615f03] different name for a commit
 1 file changed, 1 insertion(+)
```

### 3. Зміни до останнього коміту за допомогою --amend:

Що б змінити останній коміт, додавши до нього новий файл, використаємо параметр `git commit --amend`

```bash
dana2@PC:~/lababa1/dubik$ git status
On branch main
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
dana2@PC:~/lababa1/dubik$ vim new2.txt
dana2@PC:~/lababa1/dubik$ git add new2.txt
dana2@PC:~/lababa1/dubik$ git commit --amend -m "create new file and new2 file"
[main a5e7027] create new file and new2 file
 Date: Wed Jan 24 12:51:09 2024 +0200
 2 files changed, 2 insertions(+)
 create mode 100644 new.txt
 create mode 100644 new2.txt
dana2@PC:~/lababa1/dubik$ git status
On branch main
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```
### 4. Об'єднання кількох останніх комітів за допомогою git reset:

Що б об'єднати кілька останніх комітів скористаємося `git reset HEAD~n`, де n = 2

```bash
dana2@PC:~/lababa1/dubik$ git reset HEAD~2
Unstaged changes after reset:
M       main.c
dana2@PC:~/lababa1/dubik$ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   main.c

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        new.txt
        new2.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Так ми відкатили зміни, що робили вище.
### 5. Видалення файлів:

Що б видалити файл, необхідно фізично видалити його, та заіндексувати цю "зміну"

```bash
dana2@PC:~/lababa1/dubik$ rm new2.txt
dana2@PC:~/lababa1/dubik$ git status -uno
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   main.c
        deleted:    new2.txt

no changes added to commit (use "git add" and/or "git commit -a")
dana2@PC:~/lababa1/dubik$ git add new2.txt
dana2@PC:~/lababa1/dubik$ git status -uno
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted:    new2.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   main.c

Untracked files not listed (use -u option to show untracked files)
```

Також можна видаляти швидше за допомогою `git rm`

```bash
dana2@PC:~/lababa1/dubik$ git rm new2.txt
rm 'new2.txt'
dana2@PC:~/lababa1/dubik$ git status -uno
On branch main
Your branch and 'origin/main' have diverged,
and have 1 and 1 different commits each, respectively.
  (use "git pull" to merge the remote branch into yours)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted:    new2.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   main.c

Untracked files not listed (use -u option to show untracked files)
dana2@PC:~/lababa1/dubik$ git commit -m "deleted new2 file"
[main 4983315] deleted new2 file
 1 file changed, 1 deletion(-)
 delete mode 100644 new2.txt
```
### 6. Переміщення файлів:

Що б перемістити (перейменувати) файл використаємо `mv`

```bash
dana2@PC:~/lababa1/dubik$ mv old.txt new.txt
dana2@PC:~/lababa1/dubik$ git status -uno
On branch main
Your branch and 'origin/main' have diverged,
and have 2 and 1 different commits each, respectively.
  (use "git pull" to merge the remote branch into yours)

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   main.c
        deleted:    old.txt

no changes added to commit (use "git add" and/or "git commit -a")
dana2@PC:~/lababa1/dubik$ git add new.txt
dana2@PC:~/lababa1/dubik$ git status -uno
On branch main
Your branch and 'origin/main' have diverged,
and have 2 and 1 different commits each, respectively.
  (use "git pull" to merge the remote branch into yours)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   new.txt

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   main.c
        deleted:    old.txt

Untracked files not listed (use -u option to show untracked files)
dana2@PC:~/lababa1/dubik$ git add old.txt
dana2@PC:~/lababa1/dubik$ git status -uno
On branch main
Your branch and 'origin/main' have diverged,
and have 2 and 1 different commits each, respectively.
  (use "git pull" to merge the remote branch into yours)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        renamed:    old.txt -> new.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   main.c

Untracked files not listed (use -u option to show untracked files)
dana2@PC:~/lababa1/dubik$ git commit -m "renamed old.txt to new.txt"
[main 7d19a20] renamed old.txt to new.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename old.txt => new.txt (100%)
```

Також можна використати `git mv`, це швидший метод

```bash
dana2@PC:~/lababa1/dubik$ git mv old.txt new.txt
dana2@PC:~/lababa1/dubik$ git status -uno
On branch main
Your branch and 'origin/main' have diverged,
and have 2 and 1 different commits each, respectively.
  (use "git pull" to merge the remote branch into yours)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        renamed:    old.txt -> new.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   main.c

Untracked files not listed (use -u option to show untracked files)
```
### 7. Гілкування:

Переглянемо наявні локальні та віддалені гілки

```bash
dana2@PC:~/lababa1/dubik$ git branch
* main
dana2@PC:~/lababa1/dubik$ git branch -a
* main
  remotes/origin/HEAD -> origin/main
  remotes/origin/main
```

Як видно, у нас існують лише стандартні гілки
#### 7.1. Створення та переключення між гілками:

Застосуємо зразу дві команди `git branch my-local-branch-1` та `git checkout -b my-local-branch-2` для демонстрації функціоналу

```bash
dana2@PC:~/lababa1/dubik$ git branch my-local-branch-1
dana2@PC:~/lababa1/dubik$ git checkout -b my-local-branch-2
Switched to a new branch 'my-local-branch-2'
dana2@PC:~/lababa1/dubik$ git branch
  main
  my-local-branch-1
* my-local-branch-2
```
#### 7.2. Переключення між гілками:
Застосуємо команду `git checkout` що б змінити активну гілку

```bash
dana2@PC:~/lababa1/dubik$ git checkout my-local-branch-1
M       main.c
A       new.txt
D       old.txt
Switched to branch 'my-local-branch-1'
```

### 8. Робота з логами гіту

Використаємо репозиторій з першого пункту, там є хороша історія змін

Виконуємо команду `git log`

```bash
dana2@PC:~/lababa1$ cd refine
dana2@PC:~/lababa1/refine$ ls
CHANGELOG.md        README.md             documentation   lerna.json         package.json         typos.toml
CODE_OF_CONDUCT.md  SECURITY.md           examples        logo.png           packages
CONTRIBUTING.md     commitlint.config.js  hackathon       nx.json            tsconfig.build.json
LICENSE             cypress               jest.config.js  package-lock.json  tsconfig.json
dana2@PC:~/lababa1/refine$ git log
commit 872119f44a4a82b2d6327ea218361a38628a7dc6 (HEAD -> master, origin/master, origin/HEAD)
Author: Ömer Faruk APLAK <omer@pankod.com>
Date:   Tue Jan 23 17:01:42 2024 +0300

    chore: typo fix

commit aa4e0f67dce846f58d054b003f28b5f0269bfdfe
Author: Batuhan Wilhelm <batuhanwilhelm@gmail.com>
Date:   Tue Jan 23 16:31:50 2024 +0300

    chore: run audit-fix in root (#5545)

commit 37a7ea59424bc561df6b2f714e70825531cda332
Author: Ali Emir Şen <senaliemir@gmail.com>
Date:   Tue Jan 23 15:42:04 2024 +0300

    chore(examples): update scripts and cross-env

commit 840442cbba0149cde219118d33eeb52920e633db
Author: Batuhan Wilhelm <batuhanwilhelm@gmail.com>
Date:   Tue Jan 23 13:08:09 2024 +0300

    docs: add refine with existing projects guide (#5521)

commit d539417e00cb5e775394c7496f940221f4dc55fc
Author: Imanuel Pundoko <ilomon10@gmail.com>
Date:   Tue Jan 23 18:07:05 2024 +0800

    [DOC] Add FAQ about working offline locally (#5544)
```

Використаємо команду, яка покращує формат виведення `git log 840442cbba0149cde219118d33eeb52920e633db..HEAD --format="%h %as '%s'"`

```bash
dana2@PC:~/lababa1/refine$ git log 840442cbba0149cde219118d33eeb52920e633db..HEAD --format="%h %as '%s'"
872119f44a 2024-01-23 'chore: typo fix'
aa4e0f67dc 2024-01-23 'chore: run audit-fix in root (#5545)'
37a7ea5942 2024-01-23 'chore(examples): update scripts and cross-env'
```

Використаємо команду `git log -G "Quick Start" README.md`, що б знайти коли до файлу README.md додали пункт "Quick Start"

```bash
dana2@PC:~/lababa1/refine$ git log -G "Quick Start" README.md
commit 02b724e97406fdfe5ac24f986265f9ea701b552f
Author: Muharrem Kocadere <mkocadere@gmail.com>
Date:   Fri Aug 20 10:46:46 2021 +0300

    Add overview to readme (#1025)

    * add overview to readme

    Co-authored-by: Necati Özmen <necatiozmn@gmail.com>

    * add badges

    Co-authored-by: Necati Özmen <necatiozmn@gmail.com>
```

За допомогою команди `git diff 02b724e97406fdfe5ac24f986265f9ea701b552f~..02b724e97406fdfe5ac24f986265f9ea701b552f README.md` дізнаємося зміни файлу в цьому конкретному коміті

```bash
dana2@PC:~/lababa1/refine$ git diff 02b724e97406fdfe5ac24f986265f9ea701b552f~..02b724e97406fdfe5ac24f986265f9ea701b552f
diff --git a/README.md b/README.md
index 6203901bde..6085591ffb 100644
--- a/README.md
+++ b/README.md
@@ -1,30 +1,209 @@
-# refine
+<div align="center" style="margin: 30px;">
+<a href="https://pankod.github.io/superplate/">
+  <img src="documentation/static/img/refine_logo.png"  align="center" />
+</a>
+</div>
+<br/>
+<div align="center"><strong>refine</strong> is a <a href="https://reactjs.org/">React</a>-based framework for building data-intensive applications in no time ✨ It ships with <a href="https://ant.design/">Ant Design System</a>, an enterprse-level UI toolkit.</div>
+<br/>

+<div align="center">

-[![NPM](https://img.shields.io/npm/v/@pankod/refine.svg)](https://www.npmjs.com/package/@pankod/refine) [![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com) [![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-2.0-4baaaa.svg)](code_of_conduct.md)
+[![Meercode CI Score](https://meercode.io/badge/pankod/superplate?type=ci-score&branch=master&token=2ZiT8YsoJgt57JB23NYwXrFY3rJHZboT&lastDay=31)](https://meercode.io/)
+[![Meercode CI Success Rate](https://meercode.io/badge/pankod/superplate?type=ci-success-rate&branch=master&token=2ZiT8YsoJgt57JB23NYwXrFY3rJHZboT&lastDay=31)](https://meercode.io/)
+[![Maintainability](https://api.codeclimate.com/v1/badges/eb4b5a8f88b6e511e61d/maintainability)](https://codeclimate.com/github/pankod/refine/maintainability)
+[![npm version](https://img.shields.io/npm/v/@pankod/refine.svg)](https://www.npmjs.com/package/@pankod/refine)
:
```

Також це можна зробити швидше командою `git show 02b724e97406fdfe5ac24f986265f9ea701b552f README.md`

```bash
dana2@PC:~/lababa1/refine$ git show 02b724e97406fdfe5ac24f986265f9ea701b552f README.md
commit 02b724e97406fdfe5ac24f986265f9ea701b552f
Author: Muharrem Kocadere <mkocadere@gmail.com>
Date:   Fri Aug 20 10:46:46 2021 +0300

    Add overview to readme (#1025)

    * add overview to readme

    Co-authored-by: Necati Özmen <necatiozmn@gmail.com>

    * add badges

    Co-authored-by: Necati Özmen <necatiozmn@gmail.com>

diff --git a/README.md b/README.md
index 6203901bde..6085591ffb 100644
--- a/README.md
+++ b/README.md
@@ -1,30 +1,209 @@
-# refine
+<div align="center" style="margin: 30px;">
+<a href="https://pankod.github.io/superplate/">
+  <img src="documentation/static/img/refine_logo.png"  align="center" />
+</a>
+</div>
+<br/>
+<div align="center"><strong>refine</strong> is a <a href="https://reactjs.org/">React</a>-based framework for building data-intensive applications in no time ✨ It ships with <a href="https://ant.design/">Ant Design System</a>, an enterprse-level UI toolkit.</div>
```
