## Monorepo Test

This monorepo contains 3 "projects". Each project has .dat files containing random data of different sizes:

* `project1` contains a 10MB .dat file
* `project2` contains a 15MB .dat file
* `project3` contains a 2MB .dat file

### Checking out only one project

You can use a combination of `git clone --filter` and `git sparse-checkout` to only retrieve one project's 
files. For example, to retrieve only `project1`:

```
git clone -n --depth=1 --filter=tree:0 https://github.com/jamescarppe/monorepo.git
cd monorepo
git sparse-checkout set --no-cone project1
git checkout
```

Only the `project1` directory will be retrieved.

You can use a `du` to confirm that only the requested project was downloaded:

```
:~/git/monorepo$ du --apparent-size -hs *
11M     project1
```

As compared to the full repo:

```
~/git/monorepo$ du --apparent-size -hs *
208     README.md
11M     project1
16M     project2
2.1M    project3
```

### Sources

This was based off [this answer](https://stackoverflow.com/a/52269934) on Stack Overflow. Further reading 
is contained within.
