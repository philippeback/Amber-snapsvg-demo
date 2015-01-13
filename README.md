# Amber Smalltalk Snap.svg Demo

Demo how to use the [Snapsvg libary](http://snapsvg.io/) in Amber Smalltalk 0.14.1

## Getting Started

To bring project alive (for example after `git clone`):

```sh
npm install
bower install
grunt devel
```

Developing the project (after brought alive):
 
Start server with `amber serve` and go to `http://localhost:4000/` in your browser and follow the instructions


## How was this constructed


### amber init



    hanneshirzel@hanneshirzel-Latitude-E6410 ~/Amber-snapsvg-demo $ amber init
    Welcome to Amber version 0.14.0 (NodeJS 0.10.25).
    Running "init:/usr/local/lib/node_modules/amber-cli/node_modules/grunt-init-amber" (init) task
    This task will create one or more files in the current directory, based on the
    environment and the answers to a few questions. Note that answering "?" to any
    question will show question-specific help and answering "none" to most questions
    will leave its value blank.
    
    "grunt-init-amber" template notes:
     Project title should be a human-readable title.
    
    Please answer the following:
    [?] Project title (Application or Library Title) Amber Smalltalk Snap.svg Demo
    [?] Main class and package of Amber application.
    Project name is derived by lowercasing this. (AmberSmalltalkSnapSvgDemo) AmberSnapsvg
    [?] Description (The Application or The Library doing The Thing.) Demo how to use the Snapsvg libary in Amber Smalltalk
    [?] Author name (hhzl) 
    [?] Author email (hannes.hirzel@gmail.com) 
    [?] Namespace of the new Amber package. (amber-ambersnapsvg) amber-snapsvg
    [?] Version (0.1.0) 
    [?] Project git repository (git://github.com/hanneshirzel/Amber-snapsvg-demo.git) 
    [?] Project homepage (https://github.com/hanneshirzel/Amber-snapsvg-demo) 
    [?] Project issues tracker (https://github.com/hanneshirzel/Amber-snapsvg-demo/issues) 
    [?] Author url (none) 
    [?] Licenses (MIT) 
    [?] Do you need to make any changes to the above before continuing? (y/N) 


### Installation of snap.svg

    bower install snap.svg --save


Creation of snap.svg.amd.json


    {
    "paths": {
                "snap.svg" : "dist/snap.svg"
             }
    }


Add it to ``deploy.js``


    define([
        'amber/deploy',
        'snap.svg',
        // --- packages to be deployed begin here ---
        'amber-snapsvg/AmberSnapsvg'
        // --- packages to be deployed end here ---
    ], function (amber) {
        return amber;
    });

Generate new ``config.js`` with

    grunt devel


Check that the library is properly referenced in ``config.js``


    "snap.svg": "bower_components/snap.svg/dist/snap.svg",



### Add Smalltalk code

Add a #snapsvg-button to the ``index.html`` page


Change method #augmentPage to

    augmentPage
	'#amber-with' asJQuery click: [ self doAmberWith ].
	'#jquery-append' asJQuery click: [ self doJQueryAppend ].
	'#snapsvg-button' asJQuery click: [self doSnapSvg]

Create a method #doSnapSvg

    doSnapSvg
    "translation to Smalltalk points 1 to 4 of
    http://snapsvg.io/start/ "
    
    | s bigCircle smallCircle |
        
    s := Snap value: 300 value: 600.
    bigCircle := s circle: 150 value: 150 value: 100.
    bigCircle attr: #{'fill' -> '#bada55'. 'stroke' -> '#000'. 'strokeWidth' -> 5}.
    smallCircle := s circle: 100 value: 150 value: 70.

