#### Check your progress

You probably saw something like this when you ran `scmake()`:

```
> library(scipiper)
USGS Support Package: https://owi.usgs.gov/R/packages.html#support
> scmake()
Starting build at 2020-06-08 12:24:55
<  MAKE > main
[ BUILD ] states                              |  states <- c(c("AL", "AZ", "AR", "CA", "CO", "CT",...
[  READ ]                                     |  # loading packages
[ BUILD ] parameter                           |  parameter <- c("00010")
[ BUILD ] oldest_active_sites                 |  oldest_active_sites <- find_oldest_sites(states, ...
  Inventorying sites in AL
  Inventorying sites in AZ
  ...
  Inventorying sites in HI
  Inventorying sites in PR
[ BUILD ] state_combiners                     |  state_combiners <- do_state_tasks(oldest_active_s...
v0.0.17: tickquote_combinee_objects is deprecated and will effectively be always TRUE in future versions
Run all tasks and finalizers with:
obs_tallies:
  command: scmake(I('obs_tallies_promise'), remake_file='/Users/aappling/Documents/Code/Pipeline/ds-pipelines-3-temp2/123_state_tasks.yml')
3_visualize/out/timeseries_plots.yml:
  command: scmake(I('timeseries_plots.yml_promise'), remake_file='/Users/aappling/Documents/Code/Pipeline/ds-pipelines-3-temp2/123_state_tasks.yml')
All tasks complete [==============================================================================] 100%  

### Final check for completeness of all targets
Starting build at 2020-06-08 12:25:31
<  MAKE > 123_state_tasks
[    OK ] parameter
[ BUILD ] AL_data                             |  AL_data <- get_site_data("1_fetch/tmp/inventory_A...
[  READ ]                                     |  # loading packages
  Retrieving data for AL-02397530
Error in get_site_data("1_fetch/tmp/inventory_AL.tsv", parameter) : 
  Ugh, the internet data transfer failed! Try again.
In addition: Warning messages:
1: package ‘tibble’ was built under R version 3.6.2 
2: package ‘tidyr’ was built under R version 3.6.2 
3: package ‘purrr’ was built under R version 3.6.2 
 Error in get_site_data("1_fetch/tmp/inventory_AL.tsv", parameter) : 
  Ugh, the internet data transfer failed! Try again. 
```

The build may not have failed on `AL`, but it almost certainly failed before pulling data for all the sites, right? And we've somehow lost the fault tolerance that `loop_tasks` is supposed to provide.

So what happened? Well, the first part is good news: when you changed `parameter` and `states`, **scipiper** correctly noticed the need to rebuild first the inventory (`oldest_active_sites`) and then the task table (`state_combiners`). But then rather than launching into
```
### Starting loop attempt 1 of 30...
```
as you might have hoped, the build of the task table jumped straight to 
```
All tasks complete [==============================================================================] 100%  

### Final check for completeness of all targets
Starting build at 2020-06-08 12:25:31
...
```
The `loop attempt`s include fault tolerance (i.e., if one task fails, moving onto the next task without throwing and error, then returning to the failed task in the next loop). But the `Final check` is essentially a call to `scmake()` to make sure those loops resulted in a fully built task table. `loop_tasks()` uses a heuristic (shortcut algorithm) to guess whether loop attempts are needed: it looks for the presence of the 

### :keyboard: Activity: Push the limits of `loop_tasks`

Switching to temperature creates a need for force=TRUE to take advantage of the fault tolerance - the rebuild happens, but it jumps straight to the final check

### :keyboard: Activity: Repurpose the pipeline



#### Test

- [ ] Run `library(scipiper)` (because you're in a new R session) and then `scmake()`. Note the different console messages this time.

Comment on what you're seeing. 

<hr><h3 align="center">I'll respond when I see your comment.</h3>

