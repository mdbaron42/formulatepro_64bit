# FormulatePro
FormulatePro is a small (but very useful) utility to allow one to add text and images to PDF versions of forms, whch can then be saved or printed. I personally find it more useful than trying to do this in Preview. The original application is only available as a 32-bit app, so I downloaded the source code from _adlr/formulatepro_ and compiled it as a 64-bit app when I finally moved up from OSX Mojave. 

I recently had to do this again with Xcode 13 and found it a bit of a faff, so I forked the original repository to (a) provide a version with a working .xcodeproj file for recompiling as a 64-bit app, and (b) list the changes I had to make in the Xcode project in case anyone needs to do this again in the future (although no doubt future versions of Xcode will make it even more difficult!)

## The recompiled app
I have also uploaded the recompiled application in case anyone is just looking for a version that works on a more recent version of MacOS X. I have used it on Big Sur, but haven't tested it on any computer running a newer OS or with Apple Silicon, so this is compiled for x86_64, not as a _Universal_ app.

## Compiling
To get this to compile and build, I did the following:
1) Set the project to MacOS 10.10 (well, this is optional, it could have been for an even earlier target).
2) When Xcode wanted to fix many things it did not like in the original project file, I did not allow it to code sign the Sparkle framework, did not set the ARCHS to the default, and did not allow Xcode to reconfigure the localizations.
3) Set the project architecture to x86_64 and the target build architecture to this as well.
4) Set the Base SDK tot he default (MacOS).
5) Set the compiler to the default (Apple Clang).
6) In the section about Apple Clang, change "Treat Warnings as Errors" to NO. This is very important, as there will be a lot of warnings about deprecated functions.
7) In the Build Settings, search for Code signing and find the line "Other code signing flags": add the flag **--deep**. If this is not done there is a fatal error when Xcode tries to code sign the Sparkle framework.
8) Go to the Product menu and select Scheme -> Edit Scheme, and set the "Run" build scheme to build the Release version.

All of those changes are already done in the .xcodeproj folder in this repository. It should now build successfully, although there are a great many warnings about deprecated functions, plus a couple of warnings about incorrectly cast variables that I felt could be ignored as they must have been there in the original compiled app, and it was not worth my time learning Obj C to fix them ;-)

## Big thank you to adlr for the original app!
