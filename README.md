# Calculadora
Primer ejercicio interfaz grafica
import tkinter as tk
from tkinter import ttk
from tkinter import messagebox

n = 0

def init_window():
    window = tk.Tk()
    window.title('Mi primera APP')
    window.geometry('400x250')

    label = tk.Label(window, text = 'Calculadora', font = ('Arial bold', 15))
    label.grid(column = 0, row = 0)

    label_entrada1 = tk.Label(window, text = 'Ingrese primer numero', font = ('Arial bold', 10))
    label_entrada1.grid(column = 0, row = 1)

    label_entrada2 = tk.Label(window, text = 'Ingrese segundo numero', font = ('Arial bold', 10))
    label_entrada2.grid(column = 0, row = 2)

    entrada1 = tk.Entry(window, width = 10)
    entrada2 = tk.Entry(window, width = 10)    

    entrada1.focus()
    entrada2.focus()

    entrada1.grid(column = 1, row = 1)
    entrada2.grid(column = 1, row = 2)

    label_operador = tk.Label(text = 'Escoja un operador', font = ('Arial bold', 10))
    label_operador.grid(column = 0, row = 3)

    combo_operadores = ttk.Combobox(window)
    combo_operadores['values'] = ('+', '-', '*', '/', 'pow')
    combo_operadores.current(0)
    combo_operadores.grid(column = 1, row = 3)

    label_resultado = tk.Label(text = 'Resultado: ', font = ('Arial bold', 15))
    label_resultado.grid(column = 0, row = 5)

    boton = tk.Button(window, command = lambda: click_calcular(label_resultado, entrada1.get(), entrada2.get(), combo_operadores.get()), text = 'Calcular', bg = 'red', fg = 'white')
    boton.grid(column = 1, row = 4)

    boton_ven = tk.Button(window, command = nueva_ventana, text = 'Nueva Ventana')
    boton_ven.grid(column = 3 , row = 6)

    window.mainloop()

def calculadora(num1, num2, operador):
    if operador == '+':
        resultado = num1 + num2
    elif operador == '-':
        resultado = num1 - num2
    elif operador == '*':
        resultado = num1 * num2
    elif operador == '/':
        resultado = num1 / num2
    elif operador == 'pow':
        resultado = num1 ** num2
    
    return resultado

def click_calcular(label, num1, num2, operador):
    valor1 = float(num1)
    valor2 = float(num2)

    res = calculadora(valor1, valor2, operador)
    label.configure(text = 'Resultado: ' + str(res))

def nueva_ventana():
    global n
    n += 1
    if n == 1:
        window = tk.Tk()
        window.title('Nueva pestaña')
        window.geometry('300x150')
        window.configure(background = 'red')
    if n != 1:
        messagebox.showinfo('ATENCION', 'NO PUEDES CREAR MAS VENTANAS')

def main():
    init_window()

main()
