# New architecture 
Thinking of the way I have organized the project makes me feel it lacks 
modularity. Due to this the first effort would be to move the include
folder contents inside src itself.

Renaming src to lib would be most appropriate unless a code is target 
specific.

## What makes a different target?
Meditating a bit on this weary subject, a few ideas come to mind:
1. different MCU
2. different OS

For now, the reorg will try moving the platform dependent functions 
outside the lib section. For example, I2C calls. 

## How do you organize an embedded C project
In my limited experience in embedded systems development, I have felt 
that the initial organization of files dictates how the project can 
progress. If it isn't simple or is too cluttered, it leads to a lot of
time in onboarding new developers entering a program. At least the most
simplest thing you could do is organize the project with some fundamental
rules. Lets try to organize those rules a little bit:

1. Any external dependencies should be submoduled to an `ext/` folder
2. All `lib/` can be dependent on either `ext/` or `lib/<dep>` itself
3. The build system should organize how a target is to be built
4. `app/` directory should contain the main code for that application
5. `tests/` directory should contain unit tests or other tests that the project should support
6. create a `platform` directory containing platform level support for lib

Regarding the `platform` directory definition: It somehow gets a little muddled
up when trying to define what this directory should be doing. If the app runs
the main code what should platform have? IMHO app should service what the project
can provide. For example, if one application is geared towards data collection and
another on the official release, those differences should be in the `app` code 
itself. The app should be platform agnostic. The build system should have the 
options to choose which platform you're using may it be a RP2040 or a ESP32. 

## Organizing a project using cmake
As far as I know, cmake is the easiest yet the most complicated way
to organize the system. Personally I am not well versed with its 
intricacies and I guess I need to figure out how it works. 
