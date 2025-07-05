import tkinter as tk
from tkinter import ttk

# Tasa de conversión fija
TASA_CAMBIO = 43.34

def agregar_numero(numero):
    entrada_origen.insert(tk.END, numero)

def borrar_ultimo():
    entrada_origen.delete(len(entrada_origen.get()) - 1, tk.END)

def limpiar():
    entrada_origen.delete(0, tk.END)
    entrada_destino.delete(0, tk.END)

def convertir():
    try:
        cantidad = float(entrada_origen.get())
        convertido = cantidad * TASA_CAMBIO
        entrada_destino.delete(0, tk.END)
        entrada_destino.insert(0, f"{convertido:.2f}")
    except ValueError:
        entrada_destino.delete(0, tk.END)
        entrada_destino.insert(0, "Entrada inválida")

# Configurar ventana principal
root = tk.Tk()
root.title("Conversor de Monedas")
root.resizable(False, False)

# Encabezado
tk.Label(root, text="Conversor de Monedas", font=("Helvetica", 16, "bold")).grid(row=0, column=0, columnspan=4, pady=10)

# Campos de entrada
tk.Label(root, text="De moneda (EUR):").grid(row=1, column=0, sticky="e")
entrada_origen = tk.Entry(root, justify="right")
entrada_origen.grid(row=1, column=1, columnspan=3, sticky="we", padx=5)

tk.Label(root, text="A moneda (C$):").grid(row=2, column=0, sticky="e")
entrada_destino = tk.Entry(root, justify="right")
entrada_destino.grid(row=2, column=1, columnspan=3, sticky="we", padx=5)

# Tasa de cambio
tk.Label(root, text="1 EUR = 43.34 C$", fg="gray").grid(row=3, column=0, columnspan=4, pady=5)

# Teclado numérico
botones = [
    ("7", 4, 0), ("8", 4, 1), ("9", 4, 2),
    ("4", 5, 0), ("5", 5, 1), ("6", 5, 2),
    ("1", 6, 0), ("2", 6, 1), ("3", 6, 2),
    ("0", 7, 1), (".", 7, 0), ("←", 7, 2),
]

for (texto, fila, columna) in botones:
    if texto == "←":
        comando = borrar_ultimo
        color_fondo = "red"
    else:
        comando = lambda x=texto: agregar_numero(x)
        color_fondo = "white"
    tk.Button(root, text=texto, width=5, command=comando, bg=color_fondo).grid(row=fila, column=columna, padx=2, pady=2)

# Botones funcionales
tk.Button(root, text="Convertir", width=13, command=convertir, bg="lightblue").grid(row=8, column=0, columnspan=2, pady=15)
tk.Button(root, text="Limpiar", width=13, command=limpiar, bg="lightgreen").grid(row=8, column=2, columnspan=2, pady=15)

root.mainloop()
