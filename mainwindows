import tkinter as tk
from pynput.keyboard import Controller,Key
import ctypes
from ctypes import wintypes

textcol="#e5e5e7"
fbtncol="#0A0021"
bgcol="#121212"
activecol='#27327a'
btncol="#0C076C"
sbtncol="#0054F1"

top=["F1", "F2", "F3", "F4", "F5", "F6", "F7", "F8", "F9", "F10", "F11", "F12"]
keys = [
    ['`', '1', '2', '3', '4','5','6','7','8','9','0','-','=',"Backspace"],
    ["Tab","q", "w", "e", "r", "t", "y", "u", "i", "o", "p","[","]"],
    ["Caps Lock","a", "s", "d", "f", "g", "h", "j", "k", "l",";","'", "Enter"],
    ["Shift","z", "x", "c", "v", "b", "n", "m", ",", ".", "/","↑","\\"],
    ["Ctrl","Super","Alt","Spacebar","←", "↓", "→"]
]
mapping={
    "`":"~","1": "!", "2": "@", "3": "#", "4": "$", "5": "%",
    "6": "^", "7": "&", "8": "*", "9": "(", "0": ")",
    "-": "_", "=": "+", "[": "{", "]": "}", ";": ":",
    "'": '"', ",": "<", ".": ">", "/": "?","\\":'|'
}
keymap={'Ctrl':Key.ctrl,'Super':Key.cmd,'Alt':Key.alt,'Shift':Key.shift}
buttons={}
isShift=False
isCaps=False
heldkeys=[]


def start_drag(event):
    root.x = event.x
    root.y = event.y
def do_drag(event):
    deltax = event.x - root.x
    deltay = event.y - root.y
    x = root.winfo_x() + deltax
    y = root.winfo_y() + deltay
    root.geometry(f"+{x}+{y}")

def press_key(key):
    global isShift
    global isCaps
    global heldkeys
    if key in ['Ctrl','Super','Alt','Shift']:
        target=keymap[key]
        if target in heldkeys:
            keyboard.release(target)
            heldkeys.remove(target)
            if key == 'Shift': isShift = False

        else:
            keyboard.press(target)
            heldkeys.append(target)
            if key == 'Shift': isShift = True
        updateui()
    elif key in ["↑", "↓", "←", "→"]:
            arrow_map = {
                "↑": Key.up,
                "↓": Key.down,
                "←": Key.left,
                "→": Key.right
            }
            target = arrow_map[key]
            keyboard.press(target)
            keyboard.release(target)
    else:
        if key=="X":
            for mod in heldkeys:
                keyboard.release(mod)
            root.destroy()
            return
        elif key == "Backspace":
            keyboard.press(Key.backspace)
            keyboard.release(Key.backspace)
        elif key == "Spacebar":
            keyboard.press(Key.space)
            keyboard.release(Key.space)
        elif key == "Enter":
            keyboard.press(Key.enter)
            keyboard.release(Key.enter)
        elif key == "Tab":
            keyboard.press(Key.tab)
            keyboard.release(Key.tab)
        elif key.startswith("F") and key[1:].isdigit():
            f_key = getattr(Key, key.lower())
            keyboard.press(f_key)
            keyboard.release(f_key)
        
        elif key=='Caps Lock':

            isCaps=not isCaps
            updateui()

        else:
            if heldkeys==[] or (len(heldkeys)==1 and Key.shift in heldkeys):

                if isShift and isCaps:
                    key = mapping.get(key, key.lower())
                elif isShift:
                    key = mapping.get(key, key.upper())
                elif isCaps:
                    key = key.upper()
                if isShift:
                    keyboard.release(Key.shift)
                    heldkeys=[]
                keyboard.type(key)
                
            else:
            
                keyboard.press(key)
                keyboard.release(key)
            

        for mod in heldkeys:
            keyboard.release(mod)
        isShift=False
        heldkeys=[]
        updateui()

def updateui():
    fix=['Backspace','Spacebar','Enter','Tab','Shift','Caps Lock','Super','Alt','Ctrl',"↑", "↓", "←", "→",'F1', 'F2', 'F3', 'F4', 'F5', 'F6', 'F7', 'F8', 'F9', 'F10', 'F11', 'F12']
    for key in buttons:
        
        if key in fix:
            continue
        elif isShift and isCaps:
            newtext=mapping.get(key,key.lower())
        elif isShift:
            newtext=mapping.get(key,key.upper())
        elif isCaps:
            newtext=key.upper()
        else:
            newtext=key

        buttons[key].config(text=newtext)
    for key in ['Super','Alt','Ctrl','Shift']:
        if keymap[key] in heldkeys:
            buttons[key].config(bg='#3d1ca5')
        else:
            buttons[key].config(bg=sbtncol)

keyboard = Controller()  

root = tk.Tk()
root.attributes("-topmost", True)
root.config(bg="#121212")
root.overrideredirect(True)
root.geometry("620x200")
def apply_windows_styles():
    hwnd = ctypes.windll.user32.GetParent(root.winfo_id())
    GWL_EXSTYLE = -20
    WS_EX_NOACTIVATE = 0x08000000
    style = ctypes.windll.user32.GetWindowLongW(hwnd, GWL_EXSTYLE)
    ctypes.windll.user32.SetWindowLongW(hwnd, GWL_EXSTYLE, style | WS_EX_NOACTIVATE)
root.after(200, apply_windows_styles)

Frame=tk.Frame(root,bg=bgcol)
Frame.pack(side=tk.TOP,expand=True,fill='both')

for key in top:    
    btn = tk.Button(
            Frame,
            text=key,
            takefocus=0,
            command=lambda k=key: press_key(k),
            highlightthickness=0
            ,bg=fbtncol,fg=textcol,activebackground=activecol
        )

    btn.pack(side=tk.LEFT,expand=True,fill='both',padx=1,pady=1)
    buttons[key]=btn

drag=tk.Button(
            Frame,
            text="::",
            takefocus=0,
            bg='#252732',fg="#e5e5e7",highlightthickness=0
        )
drag.pack(side=tk.LEFT,padx=2,pady=2,fill='both',expand=True)

esc = tk.Button(
            Frame,
            text="X",
            takefocus=0,
            command=lambda k="X": press_key(k),
            bg='#252732',fg="#e5e5e7",highlightthickness=0,activebackground='red'
        )
esc.pack(side=tk.LEFT,padx=2,pady=2,fill='both',expand=True)

drag.bind("<Button-1>", start_drag)
drag.bind("<B1-Motion>", do_drag)

for row in keys:
    frame=tk.Frame(root,bg=bgcol)
    frame.pack(side=tk.TOP,expand=True,fill='both')
    for key in row:
        
        btn = tk.Button(
            frame,
            text=key,
            takefocus=0,
            command=lambda k=key: press_key(k),
            highlightthickness=0
            ,bg=btncol,fg=textcol,activebackground=activecol
        )

        btn.pack(side=tk.LEFT,expand=True,fill='both',padx=2,pady=2)
        if key in keys[-1] and key!='Spacebar':
            btn.pack_configure(expand=False,fill=None)
        buttons[key]=btn
for key in ['Backspace','Enter','Tab','Shift','Caps Lock','Super','Alt','Ctrl']:
    buttons[key].config(bg=sbtncol)

root.mainloop()
