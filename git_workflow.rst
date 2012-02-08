Configure a new machine::

  machine1> git config --global user.name "John Hunter"
  machine1> git config --global user.email jdh2358@gmail.com

  # clone the main repo
  machine1> git clone git@github.com:matplotlib/matplotlib.git matplotlib.matplotlib

  # add my fork as a remote
  machine1> git remote add jdh2358 git@github.com:jdh2358/matplotlib.git
  machine1> git fetch jdh2358

Delete branches locally and remotely (see also `git hub remotes
<http://help.github.com/remotes>`_::

  machine1> git checkout master
  Switched to branch 'master'
  machine1> git branch -D test5
  Deleted branch test5 (was 7d1ad39).
  machine1> git push jdh2358 :test5
  To git@github.com:jdh2358/matplotlib.git
   - [deleted]         test5

Fetch remote and prune dead branches::

  > git fetch jdh2358
  > git remote prune jdh2358

After fetching, remove any local tracking branches which no longer
exist on remote::

  > git fetch -p jdh2358

Create a new feature branch and push to remote::

  machine1> git checkout master
  machine1> git pull
  Already up-to-date.
  machine1> git checkout -b test6
  A	test.dat
  Switched to a new branch 'test6'
  machine1> ls > test.dat
  machine1> git add test.dat
  machine1> git commit -a -m 'playing with remotes and branches'
  [test6 8f73796] playing with remotes and branches
   1 files changed, 27 insertions(+), 0 deletions(-)
   create mode 100644 test.dat
  machine1> git push jdh2358 test6Counting objects: 4, done.
  Delta compression using up to 4 threads.
  Compressing objects: 100% (3/3), done.
  Writing objects: 100% (3/3), 464 bytes, done.
  Total 3 (delta 1), reused 0 (delta 0)
  To git@github.com:jdh2358/matplotlib.git
   * [new branch]      test6 -> test6
  machine1>

On machine1, set the branch up as a tracking branch (edit .git/config)::

  [branch "test6"]
	  remote = jdh2358
	  merge = refs/heads/test6

Now "git pull' and "git push' will operate on jdh2358/test6

On a different machine, set up a tracking branch::

  # checking out test6 in this way will create a tracking branch so 'git
  # pull' and 'git push' w/ no other args will do the right thing
  machine2> git fetch jdh2358
  machine2> git checkout -b test6 jdh2358/test6
  machine2> wc *.py > test.dat
  machine2> git commit -a -m 'updated test.dat'
  machine2> git push  # because it is a tracking branch, it pushes to jdh2358/test6


Set up an ubuntu box and check out a feature branch for "read only" ::

  # install git to checkout the mpl src code
  sudo apt-get install git

  # install the pre-reqs to build matplotlib from source
  sudo apt-get build-dep python-matplotlib

  # get the latest released branch of matplotlib
  git clone git://github.com/matplotlib/matplotlib.git matplotlib.git

  # cd into the matplotlib directory and create a branch off of the release branch to test
  cd matplotlib.git
  git checkout -b mdboom-pixel_marker origin/v1.1.x

  # pull in Michael's changes
  git pull git://github.com/mdboom/matplotlib.git pixel_marker

  # build the matplotlib source code
  python setup.py build

  # install it
  sudo python setup.py install




