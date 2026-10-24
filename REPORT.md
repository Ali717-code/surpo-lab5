# Лабораторная работа 5. bisect и cherry-pick

### $ git log --oneline
d0a6a62 c7: комментарий 7
2a1dd01 c6: комментарий 6
f70c91e c5: БАГ add
c24f9c3 c4: комментарий 4
b824c11 c3: комментарий 3
27a5516 c2: комментарий 2
49d3cb1 c1: add + test

## Автоматический bisect (git bisect run sh test.sh)

### $ git bisect run sh test.sh
running 'sh' 'test.sh'
Bisecting: 0 revisions left to test after this (roughly 1 step)
[2a1dd01818f668453212f62bc4a65568212641bb] c6: комментарий 6
running 'sh' 'test.sh'
Bisecting: 0 revisions left to test after this (roughly 0 steps)
[f70c91e73860c4e62aa9bca6e28db6ecdca2394b] c5: БАГ add
running 'sh' 'test.sh'
f70c91e73860c4e62aa9bca6e28db6ecdca2394b is the first bad commit
commit f70c91e73860c4e62aa9bca6e28db6ecdca2394b
Author: Ali717-code <guy70659@gmail.com>
Date:   Sat Oct 24 14:36:53 2026 +0300

    c5: БАГ add

 calc.py | 5 +----
 1 file changed, 1 insertion(+), 4 deletions(-)
bisect found first bad commit

## cherry-pick

### $ git cherry-pick f137c61
Auto-merging calc.py
CONFLICT (content): Merge conflict in calc.py
error: could not apply f137c61... hotfix: исправление add
hint: After resolving the conflicts, mark them with
hint: "git add/rm <pathspec>", then run
hint: "git cherry-pick --continue".
hint: You can instead skip this commit with "git cherry-pick --skip".
hint: To abort and get back to the state before "git cherry-pick",
hint: run "git cherry-pick --abort".
hint: Disable this message with "git config set advice.mergeConflict false"

### $ git log --oneline
d0a6a62 c7: комментарий 7
2a1dd01 c6: комментарий 6
f70c91e c5: БАГ add
c24f9c3 c4: комментарий 4
b824c11 c3: комментарий 3
27a5516 c2: комментарий 2
49d3cb1 c1: add + test

### $ sh test.sh

> При cherry-pick возник конфликт в calc.py (в master есть позднее изменённые строки). Разрешён вручную: оставлен исправленный add (a + b) и комментарии c6, c7.

### $ git log --oneline (после разрешения)
dfb52b0 hotfix: исправление add
d0a6a62 c7: комментарий 7
2a1dd01 c6: комментарий 6
f70c91e c5: БАГ add
c24f9c3 c4: комментарий 4
b824c11 c3: комментарий 3
27a5516 c2: комментарий 2
49d3cb1 c1: add + test

### $ sh test.sh
тест пройден (exit 0)
