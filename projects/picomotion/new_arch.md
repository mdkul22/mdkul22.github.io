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


