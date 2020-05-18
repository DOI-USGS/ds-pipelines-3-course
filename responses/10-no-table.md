
```yaml
	Remake example without task table
	Inventory each state to find the oldest discharge gage in each of 3 states
	Map state-winner gages by age
	Note?: inventory output is an R object because why not. Might be nice to make it a file to git commit it because it’s small and important, but that’s a judgment call
	Activity: add one command for each state to pull data
	Note: inventory uses purrr::map_df = split-apply-combine

```

It's time to meet the data analysis challenge for this course! Over the next series of issues, you'll connect with the USGS NWIS (National Water Information System) web service to learn about some of the longest-running monitoring stations in USGS streamgaging history.

### :keyboard: Create a new branch

Before you edit any code, create a local branch called "three-states" and push that branch up to the remote location "origin" (which is the github host of your repository).

```
git checkout -b three-states
git push -u origin three-states
```

### :keyboard: Apply a downloaded to each state

Switch to the `three-states` branch (it already exists) with these shell commands:
```sh
git checkout three-states
```

Write three *scipiper* targets to apply `get_sites_data()` to each state in `states`. 


<hr><h3 align="center">I'll respond when you've opened a PR to merge the "three-states" branch into "master".</h3>
