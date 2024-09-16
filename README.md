# Semana13
Uso de GUI

import tkinter as tk
from tkinter import ttk

class AplicacionQuimicos:
    def __init__(self, root):
        self.root = root
        self.root.title("Gestión de Inventario de Químicos")
        self.root.geometry("500x400")
        
        # Etiqueta y campo de texto
        self.label = tk.Label(root, text="Nombre del Producto:")
        self.label.pack(pady=10)

        self.entry = tk.Entry(root, width=40)
        self.entry.pack(pady=5)

        # Botón para agregar
        self.add_button = tk.Button(root, text="Agregar", command=self.agregar_producto)
        self.add_button.pack(pady=5)

        # Botón para limpiar
        self.clear_button = tk.Button(root, text="Limpiar", command=self.limpiar_campos)
        self.clear_button.pack(pady=5)

        # Tabla para mostrar productos
        self.tree = ttk.Treeview(root, columns=("Producto"), show='headings')
        self.tree.heading("Producto", text="Producto")
        self.tree.pack(pady=20, fill="both", expand=True)

        # Almacenar productos
        self.productos = []

    def agregar_producto(self):
        producto = self.entry.get()
        if producto:
            self.productos.append(producto)
            self.tree.insert("", "end", values=(producto,))
            self.entry.delete(0, tk.END)  # Limpiar campo de texto después de agregar

    def limpiar_campos(self):
        # Limpiar entrada de texto
        self.entry.delete(0, tk.END)

        # Limpiar tabla
        for item in self.tree.get_children():
            self.tree.delete(item)

        # Vaciar lista de productos
        self.productos.clear()

# Crear ventana principal
if __name__ == "__main__":
    root = tk.Tk()
    app = AplicacionQuimicos(root)
    root.mainloop()
