Clojure Framework
=================

My set up for Clojure on Mac OS X Leopard.

Set Up Instructions
-------------------
I've detailed much of this set up in a [blog post][] but here's the short, command-line by command-line version:

Clone a copy of this project to your `~/Library/` directory:

	$ cd ~/Library
	$ git clone git://github.com/mreid/clojure-framework.git Clojure
	$ cd Clojure

Create a directory `lib`:

	$ mkdir -p ~/Library/Clojure/lib

Grab the [latest release][cljzip] of Clojure and put the jar in the `lib` directory:

	$ curl http://clojure.googlecode.com/files/clojure_20090320.zip > /tmp/clojure.zip
	$ unzip /tmp/clojure.zip -d /tmp/
	$ cp /tmp/clojure/clojure.jar lib/
	

Next, get [JLine][] to make Clojure's interactive mode nicer:

	$ curl http://internode.dl.sourceforge.net/sourceforge/jline/jline-0.9.94.zip > /tmp/jline.zip
	$ unzip /tmp/jline.zip -d /tmp/
	$ cp /tmp/jline-0.9.94/jline-0.9.94.jar lib/jline.jar
	
Make the `clj` script executable and link to it from somewhere in your `$PATH`. (I use `~/bin` and have added it to my `$PATH` in my `~/.bash_profile`):

	$ chmod u+x clj
	$ ln -s ~/Library/Clojure/clj ~/bin/clj

This next steps are optional. Only do them if you want to use libraries from clojure-contrib:

	$ git clone git://github.com/kevinoneill/clojure-contrib.git /tmp/contrib
	$ cd /tmp/contrib
	$ ant -Dclojure.jar=$HOME/Library/Clojure/lib/clojure.jar
	$ cp clojure-contrib.jar ~/Library/Clojure/lib/

[blog post]: http://mark.reid.name/sap/setting-up.clojure.html
[cljzip]: http://clojure.googlecode.com/files/clojure_20090320.zip
[jline]: http://jline.sourceforge.net/

Usage
-----

The `clj` command can be used to open an interactive session:

	$ clj
	Clojure
	user=> 

or it can be used to run a script:

	$ clj test.clj 
	Hello, Clojure!

To add extra jar files to the Clojure's classpath on a project-by-prject basis, just create a `.clojure` file in the project's directory with the text to add to the classpath. 

For example, in my `~/code/clojure/cafe` project directory, I can add the Grinder and Frother jars from the `~/code/clojure/cafe/lib` directory by putting their relative paths, separated by a colon, into a `.clojure` file:

	$ cd ~/code/clojure/cafe
	$ echo "lib/grinder.jar:lib/frother.jar" > .clojure
