In the last issue you noted some inefficiencies with writing out many nearly-identical targets within a remake.yml:
1. It's a pain (more typing and potentially a very long *remake.yml* file) to add new sites.
2. You have to run and re-run `scmake()` if any target breaks along the way.

In this issue we'll fix those inefficiencies by adopting the *task table* approach supported by **scipiper**.

### Definitions

A **task table** is a concept: the idea is that you can think of a *split-apply-combine* operation in terms of a table: each row of the table is a split (a **task**) and each column is an apply activity (a **step**). In the example analysis for this course, each row is a monitoring site and the first column contains calls to `get_site_data()` for that site. Later we'll create additional steps for tallying and plotting observations for each site. A **task step** is a cell within this conceptual table.

![Task table](https://user-images.githubusercontent.com/12039957/82352239-b1e1d680-99cb-11ea-927c-c68aee05ca47.png)

A task table is "conceptual" because it doesn't exist as a table in R. We implement it in two ways: as a **task plan**, which is a nested R list defining all the tasks and steps, and as a **task remakefile**, which is an automatically generated scipiper YAML file much like the `remake.yml` you're already working with.

**scipiper** provides three functions for creating task tables:
1. `create_task_plan()` builds an R list describing your task table
1. `create_task_step()` is used to define the individual steps to pass to `create_task_plan()`
1. `create_task_makefile()` generates a YAML file from the R list
