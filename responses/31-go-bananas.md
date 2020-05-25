### :keyboard: Activity: Create a separate inventory for each state

- [ ] Create a `1_fetch/tmp` directory. We often create `tmp` directories within phases to house data that's only important within that step. Since we already have `oldest_active_sites` as a top-level target, and the files we're about to create are redundant with that information, there's no need to store it twice in a higher-profile location like `out`. The choice between `tmp` and `out` is a judgment call generally; try `tmp` here and see how you like it.

- [ ] Head over to `123_state_tasks.R` and define a new function with this boilerplate:
```r
split_inventory <- function(summary_file, sites_info) {

}
```

- [ ] Add code to `split_inventory` to loop over the rows in oldest_active_sites and save each row to a file in the `1_fetch/tmp`. Each filename should have the form `inventory_[state].tsv` where `[state]` is the state abbreviation, e.g., `inventory_WI.tsv`. Based on the file suffix, you've probably already guessed that I'm suggesting you create files in tab-separated format. You can use the `readr::write_tsv` function for this purpose. _(Hey, we had a perfectly fine R object target with `oldest_active_sites`, and now we have to create a multitude of pesky little files just to support this whole splitting thing? Couldn't we just stick with R objects? Well...there probably is a way to split to objects, but we don't yet have a simple pattern established for it. If you develop an approach for this someday, your teammates will thank you for sharing it!)_

- [ ] Collect the filenames of the site-specific inventories in a vector within your function. Sort them alphabetically in preparation for writing the summary file. Sorting is a good habit especially in projects where the list of split-out files changes over time, because it makes it easier to visually scan the summary file in git/GitHub to see what has changed.

- [ ] Write a summary file to the path given by the `summary_file` argument. The `scipiper::sc_indicate()` function will do this for you - just pass in the desired summary filename as the `ind_file` argument and your vector of filenames as the `data_file` argument.


#### Test

When you think you've got it right, run your new function in isolation:
```r
source('123_state_tasks.R')
split_inventory(summary_file = '1_fetch/tmp/state_splits.yml', sites_info = scmake('oldest_active_sites'))
```

You should now see five files in the *1_fetch/tmp* folder:
```r
> dir('1_fetch/tmp')
[1] "inventory_IL.tsv" "inventory_MI.tsv" "inventory_MN.tsv" "inventory_WI.tsv"
[5] "state_splits.yml"
```

And the *state_splits.yml* file should look like this:
```yml
1_fetch/tmp/inventory_WI.tsv: f44e9d80d9b55b64dbe6a87dd9f6712f
1_fetch/tmp/inventory_MN.tsv: 9a09dd8f9356353c38b96da28d9ec490
1_fetch/tmp/inventory_MI.tsv: 96e1ce0835684c3eaba2f20eeb8898ee
1_fetch/tmp/inventory_IL.tsv: cfe384de2a1fe1e21ba29c793582e480
```
Your hashes probably won't match mine because the number of available site observations changes daily, but the overall YAML format should be the same.

If you're not quite there, keep editing until you have it. When you've got it, copy and paste the contents of *1_fetch/tmp/inventory_MN.tsv* into a comment on this issue.

<hr><h3 align="center">I'll respond when I see your comment.</h3>
