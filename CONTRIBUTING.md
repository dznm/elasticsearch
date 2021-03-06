Contributing to elasticsearch
=============================

Elasticsearch is an open source project and we love to receive contributions from our community — you! There are many ways to contribute, from writing tutorials or blog posts, improving the documentation, submitting bug reports and feature requests or writing code which can be incorporated into Elasticsearch itself.

Bug reports
-----------

If you think you have found a bug in Elasticsearch, first make sure that you are testing against the [latest version of Elasticsearch](https://www.elastic.co/downloads/elasticsearch) - your issue may already have been fixed. If not, search our [issues list](https://github.com/elastic/elasticsearch/issues) on GitHub in case a similar issue has already been opened.

It is very helpful if you can prepare a reproduction of the bug. In other words, provide a small test case which we can run to confirm your bug. It makes it easier to find the problem and to fix it. Test cases should be provided as `curl` commands which we can copy and paste into a terminal to run it locally, for example:

```sh
# delete the index
curl -XDELETE localhost:9200/test

# insert a document
curl -XPUT localhost:9200/test/test/1 -d '{
 "title": "test document"
}'

# this should return XXXX but instead returns YYY
curl ....
```

Provide as much information as you can. You may think that the problem lies with your query, when actually it depends on how your data is indexed. The easier it is for us to recreate your problem, the faster it is likely to be fixed.

Feature requests
----------------

If you find yourself wishing for a feature that doesn't exist in Elasticsearch, you are probably not alone. There are bound to be others out there with similar needs. Many of the features that Elasticsearch has today have been added because our users saw the need.
Open an issue on our [issues list](https://github.com/elastic/elasticsearch/issues) on GitHub which describes the feature you would like to see, why you need it, and how it should work.

Contributing code and documentation changes
-------------------------------------------

If you have a bugfix or new feature that you would like to contribute to Elasticsearch, please find or open an issue about it first. Talk about what you would like to do. It may be that somebody is already working on it, or that there are particular issues that you should know about before implementing the change.

We enjoy working with contributors to get their code accepted. There are many approaches to fixing a problem and it is important to find the best approach before writing too much code.

The process for contributing to any of the [Elastic repositories](https://github.com/elastic/) is similar. Details for individual projects can be found below.

### Fork and clone the repository

You will need to fork the main Elasticsearch code or documentation repository and clone it to your local machine. See
[github help page](https://help.github.com/articles/fork-a-repo) for help.

Further instructions for specific projects are given below.

### Submitting your changes

Once your changes and tests are ready to submit for review:

1. Test your changes

    Run the test suite to make sure that nothing is broken. See the
[TESTING](TESTING.asciidoc) file for help running tests.

2. Sign the Contributor License Agreement

    Please make sure you have signed our [Contributor License Agreement](https://www.elastic.co/contributor-agreement/). We are not asking you to assign copyright to us, but to give us the right to distribute your code without restriction. We ask this of all contributors in order to assure our users of the origin and continuing existence of the code. You only need to sign the CLA once.

3. Rebase your changes

    Update your local repository with the most recent code from the main Elasticsearch repository, and rebase your branch on top of the latest master branch. We prefer your initial changes to be squashed into a single commit. Later, if we ask you to make changes, add them as separate commits.  This makes them easier to review.  As a final step before merging we will either ask you to squash all commits yourself or we'll do it for you.


4. Submit a pull request

    Push your local changes to your forked copy of the repository and [submit a pull request](https://help.github.com/articles/using-pull-requests). In the pull request, choose a title which sums up the changes that you have made, and in the body provide more details about what your changes do. Also mention the number of the issue where discussion has taken place, eg "Closes #123".

Then sit back and wait. There will probably be discussion about the pull request and, if any changes are needed, we would love to work with you to get your pull request merged into Elasticsearch.

Please adhere to the general guideline that you should never force push
to a publicly shared branch. Once you have opened your pull request, you
should consider your branch publicly shared. Instead of force pushing
you can just add incremental commits; this is generally easier on your
reviewers. If you need to pick up changes from master, you can merge
master into your branch. A reviewer might ask you to rebase a
long-running pull request in which case force pushing is okay for that
request. Note that squashing at the end of the review process should
also not be done, that can be done when the pull request is [integrated
via GitHub](https://github.com/blog/2141-squash-your-commits).

Contributing to the Elasticsearch codebase
------------------------------------------

**Repository:** [https://github.com/elastic/elasticsearch](https://github.com/elastic/elasticsearch)

Make sure you have [Gradle](http://gradle.org) installed, as
Elasticsearch uses it as its build system. Gradle must be version 2.13 _exactly_ in
order to build successfully.

Eclipse users can automatically configure their IDE: `gradle eclipse`
then `File: Import: Existing Projects into Workspace`. Select the
option `Search for nested projects`. Additionally you will want to
ensure that Eclipse is using 2048m of heap by modifying `eclipse.ini`
accordingly to avoid GC overhead errors.

IntelliJ users can automatically configure their IDE: `gradle idea`
then `File->New Project From Existing Sources`. Point to the root of
the source directory, select
`Import project from external model->Gradle`, enable
`Use auto-import`.

The Elasticsearch codebase makes heavy use of Java `assert`s and the
test runner requires that assertions be enabled within the JVM. This
can be accomplished by passing the flag `-ea` to the JVM on startup.

For IntelliJ, go to
`Run->Edit Configurations...->Defaults->JUnit->VM options` and input
`-ea`.

For Eclipse, go to `Preferences->Java->Installed JREs` and add `-ea` to
`VM Arguments`.

Please follow these formatting guidelines:

* Java indent is 4 spaces
* Line width is 140 characters
* The rest is left to Java coding standards
* Disable “auto-format on save” to prevent unnecessary format changes. This makes reviews much harder as it generates unnecessary formatting changes. If your IDE supports formatting only modified chunks that is fine to do.
* Wildcard imports (`import foo.bar.baz.*`) are forbidden and will cause the build to fail. Please attempt to tame your IDE so it doesn't make them and please send a PR against this document with instructions for your IDE if it doesn't contain them.
 * Eclipse: `Preferences->Java->Code Style->Organize Imports`. There are two boxes labeled "`Number of (static )? imports needed for .*`". Set their values to 99999 or some other absurdly high value.
 * IntelliJ: `Preferences->Editor->Code Style->Java->Imports`. There are two configuration options: `Class count to use import with '*'` and `Names count to use static import with '*'`. Set their values to 99999 or some other absurdly high value.
* Don't worry too much about import order. Try not to change it but don't worry about fighting your IDE to stop it from doing so.

To create a distribution from the source, simply run:

```sh
cd elasticsearch/
gradle assemble
```

You will find the newly built packages under: `./distribution/(deb|rpm|tar|zip)/build/distributions/`.

Before submitting your changes, run the test suite to make sure that nothing is broken, with:

```sh
gradle check
```
