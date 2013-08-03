bugreporthelper
===============

Shell script and Keyboard Maestro macro to quickly insert system information into bug reports.

### Background ###

As someone who uses a lot of different software and tends to find a lot of 'edge cases' and other bugs, I often find myself emailing software developers or filling out support tickets. Often I know it would probably be *helpful* to include information about my Mac (both the hardware and the operating system) as well as precise information about the version of the software that I'm using.

But, to be honest, I'm often too lazy to include it.

Instead I tell them that I'm using the "latest version" of Mac OS X and the "latest version" of their software. But am I? Not too long ago I realized I was running 10.8.2 on a Mac that I thought was up to date. Or what if the developer comes across my email again in a month and can't remember what version was current then? They might think "Oh, well I think I fixed that since then" but if they have the exact version number for their app, they could find out much more easily.

Which is so say: sometimes developers can be lazy too.

So I came up with an easy way to include the information without requiring much work.

### How it works ###

1. [bugreporthelper.sh] is a shell script that you can use in Terminal. Just type `bugreporthelper.sh` and it will ask you if you need information about a specific app. If you say yes, it will include version information about the app. Either way it will output relevant information about your hardware and operating system.

2. [Bug-Report-Helper.kmmacros] is a [Keyboard Maestro] macro which will do the same thing without requiring that you be in Terminal. It will prompt you for the name of the App (or PreferencePane) and look for version information. It will also insert your relevant hardware and operating system information. 


## How it looks

Here's an example of what the output would look like:

*(Note: I'm just using Fantastical as an example of an app, not suggesting that it's buggy. In fact, I don't think I've ever run into a bug with it.)*


	Version Information for: /Applications/Fantastical.app
		  CFBundleShortVersionString 1.3.9 
		  CFBundleVersion 234 

	Hardware Information:
		  Model Name: MacBook Air
		  Model Identifier: MacBookAir3,2
		  Processor Name: Intel Core 2 Duo
		  Processor Speed: 2.13 GHz
		  Number of Processors: 1
		  Total Number of Cores: 2
		  L2 Cache: 6 MB
		  Memory: 4 GB

	Operating System Information:
		  ProductName:	Mac OS X
		  OS X Version:	10.8.4
		  BuildVersion:	12E55


### Installation ##

1. [bugreporthelper.sh] - install anywhere in your $PATH and make executable (`chmod 755 bugreporthelper.sh`)

2. [Bug-Report-Helper.kmmacros] - import into Keyboard Maestro (be sure to customize the keyboard shortcut and any other trigger you might want to add.)


### Note ###

1. The Keyboard Maestro macro tries to determine whether or not it can 'paste' the output of the command into the current application. 
	* If it *can*, it will do so and then restore your previous clipboard (whatever was on there before this script ran).
	* If it *can't*, it will display a notification alerting you that it couldn't paste it, and keep the info on the pasteboard for you to manually paste wherever you want it.
	* The method for determining whether or not it can paste depends on a menu item 'Paste' being enabled. Which is to say that it is not foolproof. Let me know if it behaves particularly badly in a particular app.

2. [bugreporthelper.sh] will ask whether or not you want the information added to the clipboard. It will also save the information in a temp file (either in $TMPDIR or /tmp).

[Bug-Report-Helper.kmmacros]: Bug-Report-Helper.kmmacros

[bugreporthelper.sh]: bugreporthelper.sh

[Keyboard Maestro]: http://KeyboardMaestro.com
