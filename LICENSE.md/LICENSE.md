import sys
import time
import threading
from threading import Thread
import pygame
import os
from tkinter.filedialog import askdirectory
from tkinter.filedialog import askopenfilename

try:
    from Tkinter import *
except ImportError:
    from tkinter import *

try:
    import ttk
    py3 = 0
except ImportError:
    import tkinter.ttk as ttk
    py3 = 1

listofsongs = []
realnames = []

index = 0
global a, playing
a = 0
def directorychooser():

    directory = askdirectory()
    os.chdir(directory)
    for files in os.listdir(directory):
        if files.endswith(".mp3"):
            listofsongs.append(files)

            
    return
        
def play():
    global a, playing
    a = 0
    pygame.mixer.init()
    pygame.mixer.music.load(listofsongs[a])
    pygame.mixer.music.play()
    playing = 0

def stop():
    pygame.mixer.music.stop()
       
def pause():
    global playing
    if (playing == 0):
        pygame.mixer.music.pause()
        playing = 1

    else:
        pygame.mixer.music.unpause()
        playing = 0

    
    
def next():   
    global a
    a += 1
    pygame.mixer.music.load(listofsongs[a])
    pygame.mixer.music.play()
    root.enemyDie=pygame.mixer.Sound(listofsongs[a])
    root.enemyDie.get_volume(0.0)
     
def prev():
    global a
    a -= 1
    pygame.mixer.music.load(listofsongs[a])
    pygame.mixer.music.play()
    root.enemyDie=pygame.mixer.Sound(listofsongs[a])
    root.enemyDie.get_volume(0.0)

def vp_start_gui():
    '''Starting point when module is the main routine.'''
    global val, w, root
    root = Tk()
    
    '''This class configures and populates the rootlevel window.
        root is the rootlevel containing window.'''
    _bgcolor = '#4e4e4e'  # X11 color: 'gray85'
    _fgcolor = '#00ecec'  # X11 color: 'black'
    _compcolor = '#4e4e4e' # X11 color: 'gray85'
    _ana1color = '#4e4e4e' # X11 color: 'gray85' 
    _ana2color = '#4e4e4e' # X11 color: 'gray85' 
    font12 = "-family {Segoe UI} -size 10 -weight bold -slant "  \
        "roman -underline 0 -overstrike 0"
    font9 = "-family {Segoe UI Emoji} -size 14 -weight bold -slant"  \
        " roman -underline 0 -overstrike 0"
    font10 = "-family {Segoe UI} -size 11 -weight normal -slant "  \
        "roman -underline 0 -overstrike 0"
    font11 = "-family {Segoe UI} -size 12 -weight normal -slant "  \
        "roman -underline 0 -overstrike 0"
    font15 = "-family {Segoe UI} -size 22 -weight bold -slant "  \
            "roman -underline 0 -overstrike 0"
    font16 = "-family {Segoe UI} -size 24 -weight bold -slant "  \
            "roman -underline 0 -overstrike 0"

    root.geometry("800x400")
    root.title("LIGHT CONTROLLER")
    root.configure(relief="raised")
    root.configure(background="#757575")
    root.configure(highlightbackground="#f0f0f0f0f0f0")
    root.configure(highlightcolor="black")
    #root.configure(background="#4e4e4e")

    root.mainlabel = Label(root)
    root.mainlabel.place(relx=0.24, rely=0.0, height=81, width=434)
    root.mainlabel.configure(activebackground="#f9f9f9")
    root.mainlabel.configure(activeforeground="black")
    root.mainlabel.configure(background="#757575")
    root.mainlabel.configure(disabledforeground="#a3a3a3")
    root.mainlabel.configure(font=font16)
    root.mainlabel.configure(foreground="#00ecec")
    root.mainlabel.configure(highlightbackground="#757575")
    root.mainlabel.configure(highlightcolor="black")
    root.mainlabel.configure(foreground="#00ecec")
    root.mainlabel.configure(text='''LIGHT CONTROLLER''')

    root.Button2 = Button(root)
    root.Button2.place(relx=0.05, rely=0.4, height=34, width=47)
    root.Button2.configure(activebackground="#4e4e4e")
    root.Button2.configure(activeforeground="#00ecec")
    root.Button2.configure(background="#4e4e4e")
    root.Button2.configure(disabledforeground="#a3a3a3")
    root.Button2.configure(font=font11)
    root.Button2.configure(foreground="#00ecec")
    root.Button2.configure(highlightbackground="#4e4e4e")
    root.Button2.configure(highlightcolor="black")
    root.Button2.configure(pady="0")
    root.Button2.configure(text='''<<''')
    root.Button2.configure(width=47)

    root.Button3 = Button(root)
    root.Button3.place(relx=0.13, rely=0.4, height=34, width=47)
    root.Button3.configure(activebackground="#4e4e4e")
    root.Button3.configure(activeforeground="#00ecec")
    root.Button3.configure(background="#4e4e4e")
    root.Button3.configure(disabledforeground="#a3a3a3")
    root.Button3.configure(font=font11)
    root.Button3.configure(foreground="#00ecec")
    root.Button3.configure(highlightbackground="#4e4e4e")
    root.Button3.configure(highlightcolor="black")
    root.Button3.configure(pady="0")
    root.Button3.configure(text='''||''')

    root.Button4 = Button(root)
    root.Button4.place(relx=0.13, rely=0.3, height=34, width=47)
    root.Button4.configure(activebackground="#4e4e4e")
    root.Button4.configure(activeforeground="#00ecec")
    root.Button4.configure(background="#4e4e4e")
    root.Button4.configure(disabledforeground="#a3a3a3")
    root.Button4.configure(font=font11)
    root.Button4.configure(foreground="#00ecec")
    root.Button4.configure(highlightbackground="#4e4e4e")
    root.Button4.configure(highlightcolor="black")
    root.Button4.configure(pady="0")
    root.Button4.configure(text='''Play''')
    root.Button4.configure(width=47)

    root.Button5 = Button(root)
    root.Button5.place(relx=0.21, rely=0.4, height=34, width=47)
    root.Button5.configure(activebackground="#4e4e4e")
    root.Button5.configure(activeforeground="#00ecec")
    root.Button5.configure(background="#4e4e4e")
    root.Button5.configure(disabledforeground="#a3a3a3")
    root.Button5.configure(font=font11)
    root.Button5.configure(foreground="#00ecec")
    root.Button5.configure(highlightbackground="#4e4e4e")
    root.Button5.configure(highlightcolor="black")
    root.Button5.configure(pady="0")
    root.Button5.configure(text='''>>''')

    root.Button6 = Button(root)
    root.Button6.place(relx=0.21, rely=0.3, height=34, width=47)
    root.Button6.configure(activebackground="#4e4e4e")
    root.Button6.configure(activeforeground="#00ecec")
    root.Button6.configure(background="#4e4e4e")
    root.Button6.configure(disabledforeground="#a3a3a3")
    root.Button6.configure(font=font11)
    root.Button6.configure(foreground="#00ecec")
    root.Button6.configure(highlightbackground="#4e4e4e")
    root.Button6.configure(highlightcolor="black")
    root.Button6.configure(pady="0")
    root.Button6.configure(text='''Stop''')

    root.Button7 = Button(root)
    root.Button7.place(relx=0.05, rely=0.3, height=34, width=47)
    root.Button7.configure(activebackground="#4e4e4e")
    root.Button7.configure(activeforeground="#00ecec")
    root.Button7.configure(background="#4e4e4e")
    root.Button7.configure(disabledforeground="#a3a3a3")
    root.Button7.configure(font=font11)
    root.Button7.configure(foreground="#00ecec")
    root.Button7.configure(highlightbackground="#4e4e4e")
    root.Button7.configure(highlightcolor="black")
    root.Button7.configure(pady="0")
    root.Button7.configure(text='''Load''')
    
    root.Button7.configure(command = directorychooser)
    
    root.Button2.configure(command = prev)
    root.Button3.configure(command = pause)
    root.Button4.configure(command = play)
    root.Button5.configure(command = next)
    root.Button6.configure(command = stop)
    


    root.mainloop()
vp_start_gui()
