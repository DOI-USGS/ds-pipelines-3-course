### :keyboard: Activity: Define your rows and columns

To get you started with coding, I've added a new file to your "{{ branch }}" branch called "123_state_tasks.R". Your first job is to modify this file to define the rows and columns of your task table.

First, pull that new file into your local repo. Because you've already set up your local "{{ branch }}" branch to track the origin's "{{ branch }}" branch and already have that branch checked out, this should be as simple as:
```sh
git pull
```

Second, connect this starter function to the `remake.yml` file. It has well-formed (albeit boring) outputs already.
1. Remember how last issue you added three targets beneath the line that said `# TODO: PULL SITE DATA HERE`? Well, now you should delete those targets and replace them with a recipe that calls the `do_state_tasks()` function.
```yml
  # TODO: PULL SITE DATA HERE
  state_tasks:
    command: do_site_tasks(oldest_active_sites)
```
2. Add "123_state_tasks.R" to the `sources` section of `remake.yml`.
3. Make sure the connection works by calling `print(scmake('state_tasks'))`. You should see 
```r
$example_target_name
[1] "WI_download"

$example_command
[1] "download(I('WI'))"
```
You can call this same command as you're revising code in the next couple of steps to check your progress.

Third, define the rows by assigning a vector of state names to `task_names`. Use the argument already being passed into the `do_state_tasks()` function. You won't need much code.

Fourth, modify the existing column definition for `download_step` so that it pulls the data from NWIS for each state's oldest monitoring site:

1. Modify the `target_name` argument to `create_task_step()` so that each target (**task-step**) within this column will get a name like `WI_data`. The `target_name` argument should be a function of the form `function(task_name, step_name, ...) {}` where the body of the function constructs and returns a string for each combination of `task_name` (e.g., 'WI') and `step_name` (where we've already defined this step name to be 'download'). You can ignore the `step_name` this time. When it comes time to create the task plan (the R list), this function will get applied to each value of `task_name` in a vector of `task_names`.

2. Modify the `command` argument to `create_task_step()` so that each command within this column will look like the commands you wrote for `wi_data`, `mn_data`, and `mi_data` in `remake.yml` in the previous issue. 

Lastly, test your progress. Call `print(scmake('state_tasks'))` and paste the output into a new comment on this issue.
