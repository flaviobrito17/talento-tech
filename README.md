# talento-tech
from cachorro import Cachorro
from gato import Gato
import tkinter as tk
from tkinter import messagebox
from tkinter import ttk

# Lista global para armazenar os animais cadastrados
lista = []

def CadastrarAnimal():
    """Cadastra um animal baseado nos dados fornecidos."""
    nome = entryNome.get().strip()
    raça = entryRaça.get().strip()
    idade = entryIdade.get().strip()
    tipo = varTipo.get()

   
    if not nome or not raça or not idade:
        messagebox.showinfo("Erro", "Todos os campos devem ser preenchidos.")
        return

    if not idade.isdigit():
        messagebox.showinfo("Erro", "A idade deve ser um número válido.")
        return

    # Criação do objeto e salvamento
    if tipo == "Cachorro":
        animal = Cachorro(nome, (idade), raça)
    elif tipo == "Gato":
        animal = Gato(nome, (idade), raça)
    else:
        messagebox.showinfo("Erro", "Selecione um tipo válido.")
        return

    salvar(animal)
    messagebox.showinfo("Cadastro", f"{tipo} cadastrado com sucesso!")
    LimparCampos()

def salvar(obj):
    """Salva um objeto na lista global."""
    lista.append(obj)

def atualizaListabox():
    """Atualiza o conteúdo do Listbox."""
    listbox.delete(0, tk.END)
    for obj in lista:
        listbox.insert(tk.END, obj.mostrar())

def LimparCampos():
    """Limpa os campos de entrada após o cadastro."""
    entryNome.delete(0, tk.END)
    entryRaça.delete(0, tk.END)
    entryIdade.delete(0, tk.END)
    varTipo.set("Cachorro")


# Configuração da janela principal
janela = tk.Tk()
janela.title("Cadastro de Animais")
janela.geometry("500x300")

# Layout com Notebook
janelinha = ttk.Notebook(janela)
janelinha.grid(row=0, column=0, sticky="nsew")

tab1 = ttk.Frame(janelinha)
tab2 = ttk.Frame(janelinha)

janelinha.add(tab1, text="Cadastro",)
janelinha.add(tab2, text="Lista")

# Widgets da aba "Cadastro"
label1 = tk.Label(tab1, text="Nome", font=("", 15))
label1.grid(row=0, column=0, sticky="W", padx=10, pady=10)

entryNome = tk.Entry(tab1, font=("", 15))
entryNome.grid(row=0, column=1, sticky="nsew", padx=15, pady=10)

label2 = tk.Label(tab1, text="Raça", font=("", 15))
label2.grid(row=1, column=0, sticky="W", padx=10, pady=10)

entryRaça = tk.Entry(tab1, font=("", 15))
entryRaça.grid(row=1, column=1, sticky="nsew", padx=15, pady=10)

label3 = tk.Label(tab1, text="Idade", font=("", 15))
label3.grid(row=2, column=0, sticky="W", padx=10, pady=10)

entryIdade = tk.Entry(tab1, font=("", 15))
entryIdade.grid(row=2, column=1, sticky="nsew", padx=15, pady=10)

tk.Label(tab1, text="Tipo", font=("", 15)).grid(row=3, column=0, sticky="w", padx=10)
varTipo = tk.StringVar(value="Cachorro")
tk.Radiobutton(tab1, text="Cachorro", font=("", 15), variable=varTipo, value="Cachorro").grid(row=3, column=1, sticky="w", padx=10)
tk.Radiobutton(tab1, text="Gato", font=("", 15), variable=varTipo, value="Gato").grid(row=3, column=1, sticky="e", padx=10)

tk.Button(tab1, text="Cadastrar", font=("", 15), command=CadastrarAnimal).grid(row=4, columnspan=2, pady=10)

# Widgets da aba "Lista"
listbox = tk.Listbox(tab2, font=("", 15))
listbox.grid(row=0, column=0, sticky="nsew", padx=10, pady=10,)

tk.Button(tab2, text="Atualizar", font=("", 15), command=atualizaListabox).grid(row=1, column=0, pady=10)

# Configuração da janela
janela.rowconfigure(0, weight=1)
janela.columnconfigure(0, weight=1)

tab1.rowconfigure([0, 1, 2, 3], weight=0)
tab1.columnconfigure([0, 1], weight=1)

tab2.rowconfigure(0, weight=1)
tab2.columnconfigure(0, weight=1)


janela.mainloop()



