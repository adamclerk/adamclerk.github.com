---
layout: post
title: "Nancy with Make And Mono"
description: "Look Ma!...No Windows."
category: posts
---

Recently, I purchased a Mid 2012 MacBook Pro.  I was tired of Windows and was not looking forward to the impending upgrade to Windows 8.  So I purchased a MacBook Pro.  The specs are great.  Even more so that I've installed 16GB of ram and added a Crucial M4 SSD.  

I wanted to start using my C# skills with my MacBook.  So I began working with Make and [Mono](http://www.mono-project.com) to build [Nancy](http://www.nancyfx.org) Projects.  Nancy is a MVC framework for .NET.

To tell you the truth I'm in love.  I should have make the switch sooner.  Honestly though, I don't think I could have without Nancy.  It's a great framework that works great with Mono.  

That said I'd like to share with you my latest github repo.

## [NancyWithMonoAndMake](https://github.com/adamclerk/NancyWithMonoAndMake)

### Features
- Self Hosted Exe
- Compiled with Mono 2.10.9
- Built With GNU Make 3.81
- Simulates Nuget

All you have to do to get a site up and running is to call `make run`.

As of this writing there are a few commands.

{% highlight bash %}
#run site
make run 

#run tests
make test 

#delete bin folder contents
make clean 

#delete packages & bin
make clean all 
{% endhighlight %}

### Things to Know
The project is divided into 3 sections.

- src
- test
- host
- bin

#### src
This is where the source is.  Inside here you'll find a `DLLRef.txt`.  This is what is used to generate linking commands to the `dmcs` compiler.  

You'll also see Nancy specific folders and files

Lastly, the folder `Resources` holds text files to be converted to resource files by make.

### test
This is where the tests should go.  Inside here you'll also find another `DLLREF.txt`.  

You need to modify `makefile` to provide the command to run your tests.

### host
This is the code to run the site you've created.

### bin
This is where all the compiled dll go, like…

- site.dll
- test.dll
- host.exe
- host.exe.config
- Any Referenced DLL in DLLREF.txt

### Caveats 

#### Nuget
Right now there isn't any viable Nuget for Mono.  I hear that is changing.  But in the meantime, with some `sed` goodness, I parse the packages.config file and download the packages with `wget`.

Therefore, the Nuget packages referenced in packages.config are not processed for dependencies.  You'll have to look at the nuspec to see if there are any other packages that need to be downloaded.

#### Sloppy MakeFile
Admittedly, this is the first `makefile` I've written in a long time…the last one I wrote was probably in 2001.  I'd love to have another set of eyes on the project.
