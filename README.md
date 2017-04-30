# todo.hs
A haskell implementation of todo.txt

This application was created as a series of blog posts to cover some of the
concepts of Haskell. To go through the development process go [here][2]

## Supported Features (0.2.1)

The todo.txt file is currently hardcoded to your `$HOME` directory. The default sort is based on
priority.

**Add**

    $ todo add "Complete an example task +TodoExample"
    New Task: Complete an example task
    $ todo add "Do your homework by due:tomorrow"
    New Task: Do your homework by due:2017-04-05

Supports the format descripted in the [todo.txt format doc][1], including priority, start date,
contexts and projects.

**List**

    $ todo list
    1: Pick up milk @errands
    2: Pick up eggs @errands
    3: Pay Bills +LifeProblems
    4: Pick up dog from vet
    $ todo ls "Pick up"
    1: Pick up milk @errands
    2: Pick up eggs @errands
    4: Pick up dog from vet
    $ todo ls "Pick up" @errands
    1: Pick up milk @errands
    2: Pick up eggs @errands

The list command supports optional filters for contexts and projects. List will find matches that
contain all filter options.

**Complete**

    $ todo list
    1: Pick up milk @errands
    2: Pick up eggs @errands
    3: Pay Bills +LifeProblems
    $ todo complete 2
    Task Completed
    $ todo list
    1: Pick up milk @errands
    2: Pay Bills +LifeProblems
    $ cat todo.txt
    Pick up milk @errands
    Pay Bills +LifeProblems
    x 2016-07-30 Pick up eggs @errands

The complete/done command will change an incomplete task to completed.

**Delete**

    $ todo
    1: Do not complete this task
    2: Complete this task
    $ todo delete 1
    Task Deleted
    $ todo
    1: Complete this task
    $ cat todo.txt
    Complete this task

The delete command removes the incomplete task from your todo.txt file. Doesn't not mark complete,
just deletes the entry.

**Append/Prepend/Replace**


    $ todo
    1: Complete this
    $ todo append 1 "task tomorrow"
    Updated Task: Complete this task tomorrow
    $ todo prepend 1 "IMPORTANT"
    Updated Task: IMPORTANT Complete this task tomorrow
    $ todo replace 1 "Do stuff tomorrow"
    Updated Task: Do stuff tomorrow
    $ todo
    1: Do stuff tomorrow

**Priority**

    $ todo
    1: Example Task
    $ todo pri 1 a
    Updated Priority
    $ todo
    1: (A) Example Task
    $ todo pri 1
    Updated Priority
    $ todo
    1: Example Task

**Archive**

    $ todo
    1: Example Task
    $ todo complete 1
    Task Completed
    $ todo archive
    Completed Tasks Archived
    $ cat $HOME/todo.txt
    $ cat $HOME/done.txt
    x 2017-04-27 Example Task

**Report**

    $ todo
    1: Example Task
    2: Another Task
    $ todo complete 1
    Task Completed
    $ todo report
    Completed Tasks Archived
    Report Created: 1 1
    $ cat $HOME/report.txt
    2017-04-27T13:40:35 1 1


## Future features

- Colored output
- Regex based edits

[1]: https://github.com/ginatrapani/todo.txt-cli/wiki/The-Todo.txt-Format
[2]: https://commentedcode.org/blog/2016/07/30/haskell-project-stack-and-data-types
