## Notes on ckjm_ext
- Needed to swap out the Maven plugin version
- It must be run using JDK 8, might work with JDK 11, but will not work with JDK 16

## Relevant commands
### Primary
This will crawl one file and return text results. `jar` file must be installed in a executable directory.

```console
~$ java -jar /path_to_jar.jar /path_to_file_to_read.class
```

NOTE: If you pass -x like so, it will print XML results.
NOTE: You can pass globs like '*.jar' or '*.class' usually.

```console
~$ java -jar /path_to_jar.jar -x /path_to_file_to_read.class
```

### Searching 
This will crawl the root directory of Synapse if run in the extracted folder and return classes from activation-1.1.jar (one of the files in release 3.0.1).

```console
~$ find lib -name activation-1.1.jar -print | java -jar /path_to_jar.jar
```

### Next Steps
Need to figure out a command that will search all the files and return results. There is an [Named Link](https://www.spinellis.gr/sw/ckjm/doc/indexw.html "example")(see "Using Pipelines" section) from the primary `ckjm` application's website that seems relevant, but still working out the `sed` command that will give me what I want (which is to crawl every file in the `lib` directory of Synapse in this case and return all classes from all `jar` files).

You'd need to run this command in the Synapse root.

```console
for FILE in lib/*.jar
do
   jar tf $FILE | 
   sed -n 's/some_regex_command_idk\p'
done |
java -jar /path_to_jar.jar
```

We may be able to use the `jar tf` command + `sed` to return some results on comments in the code, but honestly, there has to be an easier way. Maybe someone with a Windows machine can see if SourceMonitor will more easily return these results.

### Prof is asking us to produce
- *TABLE* with
    - Total number of files
    - Total num lines of code (SLOC)
    - Percentage of comments made to each release
    - All complexity related metrics (max & avg)

- *TABLE* with
    - Project name & release num
    - Names of the top 5 most complex files and criteria used to identify them. Briefly discuss changes in files from one release to another

- Find 2 papers citing extracted static code metrics, explain how metrics were used


I don't think we'll be able to get all these metrics with `ckjm` which is specific to static code analysis.