from tkinter import *
from pandas import DataFrame
import numpy as np
import matplotlib.pyplot as plt
from pandas import DataFrame
import math
import pdb
root = Tk()
i = 0
# Information Weight + CG direction
L = Label(root, text=" Initiation of Calculations ")
L.grid(row=0, column=0)

w = Label(root, text="Weight")
w.grid(row=i + 1, column=0)
t_weight = Entry(root)
t_weight.grid(row=i + 1, column=1)

x_cg = Entry(root)
y_cg = Entry(root)
z_cg = Entry(root)

x = Label(root, text="X - CG")
x.grid(row=i + 2, column=0)
x_cg.grid(row=i + 2, column=1)

y = Label(root, text="Y CG")
y.grid(row=i + 3, column=0)
y_cg.grid(row=i + 3, column=1)

z = Label(root, text="Z CG")
z.grid(row=i + 4, column=0)
z_cg.grid(row=i + 4, column=1)

# Hoist #1
h1x_cg = Entry(root)
h1y_cg = Entry(root)
h1z_cg = Entry(root)

h1 = Label(root, text=" Hoist#1 X ")
h1.grid(row=i + 5, column=0)
h1x_cg.grid(row=i + 5, column=1)

h1 = Label(root, text=" Hoist#1 Y ")
h1.grid(row=i + 5, column=2)
h1y_cg.grid(row=i + 5, column=3)

h1 = Label(root, text=" Hoist#1 Z ")
h1.grid(row=i + 5, column=4)
h1z_cg.grid(row=i + 5, column=5)

# Hoist #2
h2x_cg = Entry(root)
h2y_cg = Entry(root)
h2z_cg = Entry(root)

h2 = Label(root, text=" Hoist#2 X ")
h2.grid(row=i + 6, column=0)
h2x_cg.grid(row=i + 6, column=1)

h2 = Label(root, text=" Hoist#2 Y ")
h2.grid(row=i + 6, column=2)
h2y_cg.grid(row=i + 6, column=3)

h2 = Label(root, text=" Hoist#2 X ")
h2.grid(row=i + 6, column=4)
h2z_cg.grid(row=i + 6, column=5)

# Hoist 3
h3x_cg = Entry(root)
h3y_cg = Entry(root)
h3z_cg = Entry(root)

h3x_cg.grid(row=i + 7, column=1)
h3y_cg.grid(row=i + 7, column=3)
h3z_cg.grid(row=i + 7, column=5)

h3 = Label(root, text=" Hoist#3 X ")
h3.grid(row=i + 7, column=0)
h3 = Label(root, text=" Hoist#3 Y ")
h3.grid(row=i + 7, column=2)
h3 = Label(root, text=" Hoist#3 Z ")
h3.grid(row=i + 7, column=4)

# Degrees


# Calculation of the Hoist Loads
def calculation():

    tw = float(t_weight.get())
    # Distance between CG TO H3
    h3x = float(h3y_cg.get()) - float(y_cg.get())
    h1h2x = abs(float(h1x_cg.get()) - float(h2x_cg.get()))
    h1h2d = abs(float(h1h2x) - float(x_cg.get()))
    h3load = float(t_weight.get()) * (h1h2d) / (h1h2d + (h3x))
    h1h2load = float(t_weight.get()) - h3load
    h1load = (h1h2load * (float(h2x_cg.get()) - float(h1x_cg.get())) / 2) / (float(h1x_cg.get()) + float(h2x_cg.get()))
    h2load = (h1h2load) - (h1load)

    h11load = Label(root, text=h1load)
    h22load = Label(root, text=h2load)
    h33load = Label(root, text=h3load)

    # data = { 'First Column Name' : ['Des','DSa'],
    # 'Second Column Name' : ['First Value', 'Second Value']}

    # df = DataFrame(data, columns = ['First Column Name','Second Column Name'])
    pdb.set_trace()
    print(h3x)
    print(h1h2x)
    print(h1h2d)
    print(h1h2load)
    print(h3load)
    print(h2load)
    print(h1load)

    h11load.grid(row=i + 15, column=0)
    h22load.grid(row=i + 15, column=1)
    h33load.grid(row=i + 15, column=2)

    data = {X: [h1x_cg.get(), h2x_cg.get(), h3x_cg.get(), x_cg.get()],
            Y: [h1y_cg.get(), h2y_cg.get(), h3y_cg.get(), y_cg.get()]}

    X_float = [h1x_cg.get(), h2x_cg.get(), h3x_cg.get()]
    Y_float = [h1y_cg.get(), h2y_cg.get(), h3y_cg.get()]

    X_cg_float = [x_cg.get()]
    Y_cg_float = [y_cg.get()]

    list_of_X_float = []
    list_of_Y_float = []

    list_of_x_cg = []
    list_of_y_cg = []

    for item in X_float:
        list_of_X_float.append(float(item))

    for item in Y_float:
        list_of_Y_float.append(float(item))

    for item in X_cg_float:
        list_of_x_cg.append(float(item))

    for item in Y_cg_float:
        list_of_y_cg.append(float(item))

    df = DataFrame(data, columns=[X, Y])

    print(df)
    print(list_of_X_float)
    print(list_of_Y_float)
    print(list_of_x_cg)
    print(list_of_y_cg)

    plt.plot(list_of_x_cg, list_of_y_cg, 'bo')
    plt.plot(list_of_X_float, list_of_Y_float,'ro')
    plt.show()


bu = Button(root, text=" Press me", command=calculation)
bu.grid(row=i + 14, column=0)

root.mainloop()
