### :keyboard: Activity: Use `loop_tasks`

Rather than babysitting repeated `scmake()` calls until all the states build, it's time to try another option for building a task table: the `loop_tasks()` function. Thisi function is designed to provide fault tolerance for tasks such as this data pull (including those where the "failures" are all real rather than being largely synthetic as in this project :wink:).

#### Expand `states`

- [ ] Within `do_state_tasks()`, insert a call to `loop_tasks` just before the calls to `scmake('obs_tallies')` and `scmake('timeseries_plots_info')`. Use the documentation at `?loop_tasks` to figure out how to pass in the task plan information (first two arguments); leave `task_steps=NULL` and `step_names=NULL`.

- [ ] Adjust `num_tries` if desired to make it even more likely that you'll just need one call to `scmake()` next time.

- [ ] Leave `n_cores = 1` to avoid overloading NWIS Web or your local network with multiple simultaneous HTTP requests. But note that you could set this to a higher number if your task plan included local processing tasks that would go faster with local parallelization.

- [ ] Leave the two calls to `scmake()` within `do_state_tasks()`. These are necessary for bringing the output into the local environment within `do_state_tasks`.....

#### Test

- [ ] Run `scmake()`. Note the different console messages this time.

Comment on what you're seeing. 

<hr><h3 align="center">I'll respond when I see your comment.</h3>
