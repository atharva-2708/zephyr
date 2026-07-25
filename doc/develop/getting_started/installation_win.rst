Using USB in WSL2 (Troubleshooting)
===================================

Out of the box, WSL2 cannot see physical USB devices plugged into a Windows 
machine. To be able to flash a board through WSL, a tool called ``usbipd-win`` 
is used to share the USB port from Windows over to Linux.

1. Install usbipd on Windows:
   Open PowerShell as Administrator in Windows and install the tool:

   .. code-block:: console

      winget install --interactive --exact dorssel.usbipd-win

2. Attach your board to WSL:
   Plug in your board and run these commands in Windows PowerShell to find it 
   and share it:

   .. code-block:: console

      usbipd list
      usbipd bind --busid <BUSID>
      usbipd attach --wsl --busid <BUSID>

3. Fixing WSL Permissions:
   Even after attaching the USB, Linux might give a "Permission Denied" error 
   (like on ``/dev/ttyUSB0``) when trying to flash. To fix this, add the WSL 
   user to the dialout group:

   .. code-block:: console

      sudo usermod -aG dialout $USER

   Completely close and reopen the WSL terminal after running this so the 
   permissions take effect.