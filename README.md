# leitor-virtual-suporte-pt_br-e-en
# código inteiro
# ele ficou bem cagadinho pq eu são quase 3 horas fa manhã e fiquei animado pra terminar logo

from tkinter import *
from gtts import gTTS
import os
from time import sleep

app = Tk()

app_width = 350
app_height = 100
app_left = 450
app_top = 150
app.geometry(f'{app_width}x{app_height}+{app_left}+{app_top}')
app.resizable(height = False, width = False)
app.title("Leitor virtual")
app.configure(background= "#93959e")

label = Label(app, text="Leitor Virtual")
label.place(x = 115, y = 5)
label.configure(background="#93959e")

text = Entry(app, width= 35, border=False)
text.place(x= 6, y = 25)
text.configure(background="#d2d4dd")

label2 = Label(app, text="Seja bem-vindo")
label2.place(x= 10, y=60)
label2.configure(background="#93959e")

global escolha
escolha = "pt"
global fala

def en() :
    global escolha
    escolha = "en"
    print(escolha)

def pt() :
    global escolha
    escolha = "pt"
    print(escolha)

print(escolha)

def funcao() :
    print("testando conexão")
    print(escolha)
    if text.get() != "" :
        teste = 0
        for i in range(0, 1):
            sleep(1)
            teste += 1
            if teste == 1:
                fala = text.get()

                voz = gTTS(fala, lang = f"{escolha}")
                voz.save(f"voz.mp4")

                os.system(f'mpg321 voz.mp4 &')

                label2.configure(text = "Leitura realizada com sucesso")
                botao.place(x = 220)

    else:
        voz = gTTS("Digite algo no console", lang = f"{escolha}")
        voz.save(f"vozConsole.mp4")

        os.system(f'mpg321 vozConsole.mp4 &')

        print("conexão falhada")
        label2.configure(text = "Digite algo no console")
        botao.place(x = 160)

botao = Button(app, text = "Ler", command = funcao, border=False)
botao.place(x = 135, y = 55) 
botao.configure(background="#b8b9c1")

botao_pt_br = Button(app, text = "PT", command = pt, border=False)
botao_pt_br.place(x =300, y = 20) 
botao_pt_br.configure(background="#b8b9c1", foreground="#48a000")

botao_en = Button(app, text = "EN", command = en, border=False)
botao_en.place(x = 300, y = 55) 
botao_en.configure(background="#b8b9c1", foreground="#001572")

app.mainloop()
