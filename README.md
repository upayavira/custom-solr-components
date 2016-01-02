Sample Solr Component Infrastructure
====================================

This project provides simple infrastructure for building your own Solr
components. Building components for Solr requires that they be compiled
against Solr itself, but also that a Jar file be created that contains
your code alone. This project handles all of that for you. You simply
need to tell it where to find a zip file of the appropriate version of
Solr.

This project is currently set up for Solr 5.4.0. Do not assume that it
will work for previous Solr releases, as there have been major changes
to the directory structure in the project.

Having said that, the Jar file created using this project should be
compatible with any recent Solr (so long as the interfaces you 
interact with have not changed).

Usage
-----
This project uses Apache Ant. 

### Configuring this Build
Default properties for Ant are stored in `default.properties`. To 
override these, create a `local.properties` and place your overridden
properties in that file. Properties in `local.properties` will take
precendence.

### Unpacking Solr

Either put a downloaded Zip of Solr 5.4.0 into a `downloads/` directory,
or create a `local.properties` file that points to your downloads location:

solr.downloads.dir=~/Downloads

Unpack Solr with:

    ant unzip-solr

Note, this is a one-off task. Subsequent tasks, such as building
your components do not depend upon this step because it is 
unnecessary and timeconsuming to re-unzip Solr every time you want
to recompile your components.

### Building Your Components

To produce a jar file:

    ant jar

This creates a Jar file in the `build/` directory.

### Configuring Solr
This project assumes you have Solr configs specific to your own
application. Place these configs into the `src/main/config` 
directory. You may well need to add configuration for Solr to 
locate your custom components to these files.

If you do not yet have configs for your project, Ant can create
initial versions for you with:

   ant initialise-configs

**Warning: this will overwrite your own configs if they are 
already there. Only do it when you don't have any configs of your
own.**

### Deploying your Components to a Local Solr
By default, a core called `my-collection` will be created for you.
To change the name of the default core, add a property to your
`local.properties` file:

    deploy.collection=some-other-core-name

This project is capable of running a Solr instance with your 
components enabled. To deploy your components to this local Solr:

    ant deploy

### Running Solr
There are three tasks related to running a local Solr. Their purposes
should be self-evident:

    ant start
    ant restart
    ant stop

### Debugging Solr
Components can be debugged using a Java IDE such as Eclipse or Idea.

Create a project within your IDE pointing at this codebase. You do not
need to include the source for Solr itself, although doing so will 
allow you to step into Solr code from your own.

Start solr with:

    and debug

You should then be able to connect to Solr from your IDE on port 
8000.

Should you wish to debug code within your component that runs on
startup, edit the `build.xml` file, inside the `debug` target change
`suspend=n` to `suspend=y`.

Sample Components
-----------------
Over time I expect to add samples for different component types to this
project. Please contact me if you require specific examples, or if you
need help producing initial prototypes of your Solr components.

Upayavira
