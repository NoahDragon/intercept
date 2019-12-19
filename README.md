## intercept

**Limitation**: due to free version license on Interception, [max 10 devices](https://github.com/oblitum/Interception/issues/25) per boot are allowed. 

This is a fork repo for https://www.orbiter-forum.com/showthread.php?t=30829

To work with AutoHotkey, please check the [Video](https://www.youtube.com/watch?v=y3e_ri-vOIo) and its [starter code](https://github.com/TaranVH/2nd-keyboard/tree/master/Intercept).

### Keyboard remapping for fun and profit!

- Are you dissatified with default key bindings in Orbiter?
- Do you want to use a cheap keyboard / keypad in your simpit, but feel too limited by the default layout of controls?
- Would you like to use multiple keyboards?
- Would you like to send multiple key combos with a single key press?

If yes, then this program is for you!

### Installation

The program is based on Oblitum Interception library, which performs a low-level keyboard interception using a kernel driver. For more information, see http://oblita.com/Interception.html

1. Download the installer from [Oblitum Interception](https://github.com/oblitum/Interception/releases/download/v1.0.1/Interception.zip)
2. Run the command prompt as administrator: Start Menu > All Programs > Accessories > Command prompt, right click, Run as administrator
3. Navigate to the directory, where you downloaded install-interception.exe and run install-interception.exe /install
4. Reboot the system.

### Tutorial

This tutorial assumes that you have 2 keyboards connected to your computer. We will remap the "x" key on the first keyboard to generate "foo" keystrokes, while the "x" key on the second keyboard will generate "bar".

First, start the program. If no parameters are given, it will start in interactive mode. (Use /help switch to learn more about command line parameters).

```
D:\intercept\Release>intercept

*** Keyboard Remapper v. 1
*** Based on Oblitum Interception http://oblita.com/Interception.html

Use /help for help on command-line options

Using configuration file D:\intercept\Release\keyremap.ini
```

The program configuration is kept in an .ini file referenced above. By default, it is keyremap.ini located in the current directory. To use another ini file, use /ini command line switch.

Let's list existing filters -- press "L" at the prompt:

```
(L)ist filters, (S)how/(A)dd/(R)emove filter, appl(Y) filters or (Q)uit?: l

(L)ist filters, (S)how/(A)dd/(R)emove filter, appl(Y) filters or (Q)uit?:
```

Predictably, there are none, because we are just starting. If you do that at the end of the tutorial, the output will look like that:

```
(L)ist filters, (S)how/(A)dd/(R)emove filter, appl(Y) filters or (Q)uit?: l

(1) x -> foo keyboard 1
(2) x -> bar keyboard 2

(L)ist filters, (S)how/(A)dd/(R)emove filter, appl(Y) filters or (Q)uit?:
```

Okay, let's remap the "X" key on the first keyboard, so pressing it will be equivalent to pressing F,O,O. Select the "Add" option by pressing "A":

```
(L)ist filters, (S)how/(A)dd/(R)emove filter, appl(Y) filters or (Q)uit?: a

Defining filter

Press key which will trigger the combo
```

Press "X" on the first keyboard.

```
  Trigger key: [X]↓
     Keyboard: HID\VID_046D&PID_C22D&REV_0165&MI_00
```

The macro will trigger when pressing (↓) the "X" key on keyboard with Device ID HID\VID_046D&PID_C22D&REV_0165&MI_00.

Now, time to define what the macro does:

```
Enter combo for this trigger, end with Esc
(Empty combo will inhibit trigger key)
```

Press F,O,O followed by Esc:

```
[F]↓ [F]↑ [O]↓ [O]↑ [O]↓ [O]↑
```

Both pressing (↓) and releasing (↑) keys is recorded.

Pressing just Esc (i.e. defining empty combo) will have an effect of disabling the key. This can be useful e.g. to prevent accidentally pressing the Windows key while playing.

Enter macro description...

```
Enter filter label: x -> foo keyboard 1
```

The program now displays new macro definition for you to check:

```
  Trigger key: [X]↓
     Keyboard: HID\VID_046D&PID_C22D&REV_0165&MI_00
        Combo: [F]↓ [F]↑ [O]↓ [O]↑ [O]↓ [O]↑
        Label: [x -> foo keyboard 1]

(S)ave filter or (C)ancel?:
```

Pressing "S" will save the new definition to the INI file.

Now, let us remap the "X" key on the second keyboard. Press "A" to define a new filter...

```
(L)ist filters, (S)how/(A)dd/(R)emove filter, appl(Y) filters or (Q)uit?: a

Defining filter

Press key which will trigger the combo
```

Press "X" again, but this time on the second keyboard:

```
  Trigger key: [X]↓
     Keyboard: HID\VID_046E&PID_55A5&REV_0120&MI_00
```

Notice that the device identifier is different than in the first macro!

Enter the B,A,R,Esc combo, does not matter which keyboard you use...

```
Enter combo for this trigger, end with Esc
(Empty combo will inhibit trigger key)

[B]↓ [B]↑ [A]↓ [A]↑ [R]↓ [R]↑
```

Set macro label and save...

```
Enter filter label: x -> bar keyboard 2


  Trigger key: [X]↓
     Keyboard: HID\VID_046E&PID_55A5&REV_0120&MI_00
        Combo: [B]↓ [B]↑ [A]↓ [A]↑ [R]↓ [R]↑
        Label: [x -> bar keyboard 2]

(S)ave filter or (C)ancel?: s
```

Time to activate our setup, press "Y" in the main menu:

```
(L)ist filters, (S)how/(A)dd/(R)emove filter, appl(Y) filters or (Q)uit?: y


Keyboard filters activated.
Please close this window to restore normal behavior.
To activate filters on startup, add /apply to the command line.


Running filters...
```

Now, start notepad. Press "x" on the first keyboard. You should see that "foo" gets input instead of "x". Now, press "x" on the second keyboard. This should result in inputting "bar". All other keys should work normally.

Your new key assignments will remain active as long as the program is running.
