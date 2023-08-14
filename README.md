# git-guide

### это шпаргалка, в которой будут какие-то вспомогательные команды для работы с **git** и, в целом, с командной строкой
---
### Базовые комбинация для залития измений с локального на удаленный репозиторий.
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

### Понятие хеша коммита
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

Сокращенный лог:
```bash
  git log --oneline
```

Сокращённый лог полезен, если в репозитории уже много коммитов — например, сотни или тысячи. В этом случае можно быстро найти нужный по описанию.
#### Сокращённый хеш (то есть первые несколько символов полного) можно использовать точно так же, как и полный.

Для того, чтобы выйти из просмотра лог, можно ввести **G**

**Пример описания информации о коммите:**  
![description](description_hash.png)

```bash
  HEAD
```

указывает на коммит, который был сделан последним. **Вместо хеша последнего коммита можно написать слово HEAD**

```bash
  ls
```

с помощью этой команды вы можете посмотреть содержимые файлы и папки

```bash
  cat HEAD
```

покажет содержимое файла

### Статусы файлов

1. Новые файлы в Git-репозитории помечаются как **untracked**, то есть неотслеживаемые. Git «видит», что такой файл существует, но не следит за изменениями в нём. У untracked-файла нет предыдущих версий, зафиксированных в коммитах или через команду **git add**.

2. После выполнения команды git add файл попадает в staging area, то есть в список файлов, которые войдут в коммит. В этот момент файл находится в состоянии **staged**.

3. Состояние **tracked** — это противоположность untracked. Оно довольно широкое по смыслу: в него попадают файлы, которые уже были зафиксированы с помощью git commit, а также файлы, которые были добавлены в staging area командой
```bash
  git add 
```

То есть все файлы, в которых Git так или иначе отслеживает изменения.

4. Состояние **modified** означает, что Git сравнил содержимое файла с последней сохранённой версией и нашёл отличия. Например, файл был закоммичен и после этого изменён.

**Пример изменения статуса файла:**  

```mermaid
  graph TD;
      A[untracked] -- git add --> B[staged + tracked];
      B -- git commit --> C[tracked];
      C -- изменения --> D[modified];
      D -- git add --> B;
      B -- изменения --> D;
```
#### !При добавлении изменений могут возникать конфликтные ситуации с основной веткой, чтобы этого избежать, перед началом работы на ветке, тем более перед ее созданием, необходимо забрать изменения с главной ветки, для этого необходима команда:

```bash
   git pull
```

Однако, если какие-то изменения уже производились, прежде чем воспользовать командой **git pull**, нужно скрыть эти изменения, как бы положить и в ячейку, чтобы потом достать:

```bash
   git stash
```

Полная картина будет выглядеть таким образом:

```bash
   git stash \\ скрыть изменения
   git pull  \\ забрать изменения из удаленной версии
   git stash pop  \\ добавить сокрытые изменения к локальной ветки, которая полностью идентична  теперь удаленной
```

---

### Исправление ошибок при создании неправильных коммитов до внесения их на гит:

Если вы хотите отменить последний коммит, но оставить все свои изменения в файлах, не удаляя их, необходима следующая команда:

```bash
   git reset --soft HEAD^
```
Если вы хотите вернуть состояние репозитория к предыдущему состоянию, отменив коммит с затиранием (вы удалите коммит и удалите все изменения, что внесли в коммит):

```bash
   git reset --hard <commit hash>
```
Пример:

```bash
$ git log --oneline # хеш можно найти в истории
7b972f5 (HEAD -> master) style: добавить комментарии, расставить отступы
b576d89 feat: добавить массив Expenses и цикл для добавления трат # вот сюда и вернёмся
4b58962 refactor: разделить analyzeExpenses() на countSum() и saveExpenses()

$ git reset --hard b576d89
# теперь мы на этом коммите
HEAD is now at b576d89 feat: добавить массив Expenses и цикл для добавления трат
```

*Теперь коммит b576d89 стал последним: вся дальнейшая разработка будет вестись от него. Файл также вернулся к тому состоянию, в котором был в момент этого коммита. А коммит 7b972f5 Git просто удалил.*

![delete_commit](delete_commit.png)

Однако полностью удалять коммит вовсе не обязательно, например вы могли забыть внести какие-то изменения в коммит, в таком случае достаточно просто добавить еще один файл в коммит с новыми изменениями. 

В таком случае можно внести правки в уже сделанный коммит с помощью опции **--amend** (добавить), однако важное замечание, что данная опция работает только с последним коммитом **HEAD**:

```bash
   git add common.css
   git commit --amend --no-edit
```

Опция --no-edit говорит, что сообщение коммита нужно оставить неизменным, однако хеш коммита изменится в любом случае.

Соответственно, мы можем поменять сообщение последнего коммита с помощью коммандны:

```bash
   git commit --amend -m "New message"
```

Если забыть указать у команды *git commit --amend* один из флагов (*--no-edit* или *-m*), Git предложит отредактировать сообщение коммита вручную. Для этого он откроет текстовый редактор, который установлен в системе по умолчанию. Чаще всего это либо GNU nano, либо Vim.

Если вы просто добавили лишний файл в **tracked**, вам коммандная строка сама подсказывает, что нужно просто использовать комманду:

```bash
   git restore --staged example.txt
```

Файл переместится в **untracked**.

Чтобы убрать все файлы можно использовать одну из опций:

```bash
   git restore --staged .
   git restore --staged --all
```

«Откатить» изменения, которые не попали ни в staging, ни в коммит:

```bash
   git restore <file>
```
---
### Просмотр изменений, которые были добавлны в последний коммит:

```bash
   git diff \\ просмотреть изменения в modifed
   git diff --staged \\ просмотреть изменения в staged файлах
```

```bash
   @@ -1,2 +1,2 @@ 
```
Эта строка сообщает, какие строки файла попали в сравнение. Выражение 1,2 (неважно, с плюсом или с минусом) говорит, что были использованы две строки, начиная с первой. Если бы было, например, написано +15,7, это значило бы, что в сравнении участвуют 7 строк, начиная с 15-й.

---
### Игнорирование файлов в Git

Чтобы игнорировать какие-то файлы (часто это какие-то ключи, либо настройка, возможно, проекта), необходимо поместить их в файл .gitignore - это обычный текстовый файл, он хранится в корне репозитории, и его также коммитят. В этот файл добавляются названия файлов, которые не должны помещаться на Git в открытый доступ, каждый с новой строки соответственно, либо же используют шаблоны.
Комментарии, то есть строки, начинающиеся с # Git не читает.
Также есть вот такие вспомогательные элементы:

```bash
   # игнорировать все файлы, которые заканчиваются на .jpeg
   *.jpeg

   # игнорировать все файлы "tmp" во всех подпапках папки docs
   docs/*/tmp

   # "игнорировать все файлы"
   *

   # ? - означает один символ, то есть file1.txt,file9.txt - будут игнорироваться, но file12.txt уже нет.
   file?.txt

   # игнорировать файлы file0.txt, file1.txt и file2.txt
   # при этом не игнорировать file3.txt, file4.txt, ...
   file[0-2].txt

   # игнорировать todo.txt в корне репозитория
   /todo.txt
   # для сравнения: spam.txt будет игнорироваться во всех папках
   spam.txt

   # если шаблон заканчивается слешем, то правило применится только к папке, если build название файла, то он игнорироваться не будет
   # игнорировать папку build
   build/

   # игнорировать файлы "docs/current/tmp", "docs/old/tmp",
   # а также "docs/old/saved/a/b/c/d/tmp"
   # и даже "docs/tmp", потому что ноль вложенных папок тоже подходит
   docs/**/tmp

   # игнорировать только "docs/current/tmp" и "docs/old/tmp"
   # файл "docs/old/saved/a/b/c/d/tmp" не попадает в правило
   docs/*/tmp

   # игнорировать все JPEG-файлы
   *.jpeg
   # но только не мем с Doge
   !doge.jpeg
```

Посмотреть все игнорируемые файлы можно с помощью команды:

```bash
   git status --ignored
```
---

### Работа с ветками Git
Создать ветку:

```bash
   git branch <название ветки>
```

Переключиться на нужную ветку:

```bash
   git checkout <название ветки>
```

Создать ветку и переключиться на нее:

```bash
   git checkout -b <название ветки>
```

Сравнивать ветки можно как и коммиты с помощью команды:

```bash
   git diff <название_ветки1> <название_ветки2>
```
Для облегчения этой задачи в Git есть суффикс навигации **~N**, где N — это число. Он отсчитывает от заданного коммита N коммитов назад во времени. Нумерация начинается с нуля: **commit~0** - это сам коммит, **commit~1** - предыдущий, **commit~2** — предшествующий предыдущему и так далее.
Например, **HEAD~1** — это следующий за текущим коммит. А **main~5** — это пятый коммит в ветке main, если считать с последнего выполненного коммита.
