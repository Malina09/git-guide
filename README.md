# git-guide

### это шпаргалка, в которой будут какие-то вспомогательные команды для работы с **git** и, в целом, с командной строкой
---
#### Базовые комбинация для залития измений с локального на удаленный репозиторий.
##### Для того, чтобы сделать commit требуется:<br>
1. Перепроверить все ли изменения были внесены в нужные файлы, можно использовать команду для проверки изменений на ветке:  
```bash
  git status
```

2. Добавляем измененные фыайлы в commit:
```bash
  git add *путь к файлу*
```

3. Затем пишем сообщение, которым будет сопровождаться созданный commit, сообщение должно быть кратким и отражать суть изменений файла:
```bash
  git commit -m "feat(kb): change prompt for sense"
```

4. Пушим изменения в удаленную ветку на github, обязательно проверьте куда вы хотите запушить изменения:
```bash
  git push origin main
```

---

#### Изменения добавлены!  
##### Проверить ветку, в которую вы хотите запушить изменения можно двумя способами
1. 
```bash
  git status
```
благодаря этой команде можно, в целом, посмотреть текущее состояние ветки, изменения и, естественно, будет отображено название ветки, на которой вы сейчас находитесь.

2.  
```bash
  git branch
```

---

#### Понятие хеша коммита
По сути хеш - это идентификатор коммита, то есть то, благодаря чему мы можем отличать коммиты друг от друга, в командной строке это выглядит следующим образом:
```bash
  commit 463057447f4b3ec75fc6bd3dcb150588678fba58 (HEAD -> main, origin/main, origin/HEAD)
```
Информация о коммите — это набор данных: когда был сделан коммит, содержимое файлов в репозитории на момент коммита и ссылка на предыдущий, или **родительский** (англ. parent), коммит.

[SHA Online](https://emn178.github.io/online-tools/sha1.html "Посмотри, как изменяется коммит при добавлении минимальных символов в него!")

Посмотреть информацию о коммитах можно с помощью команды:
```bash
  git log
```

**Пример описания информации о коммите:**  
![description](description_hash.png)
 
