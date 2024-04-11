import re
def criar_arquivos():
    arquivos = ['elogios.txt', 'reclamacoes.txt', 'palavras_improprias.txt']
    for arquivo in arquivos:
        if not os.path.exists(arquivo):
            open(arquivo, 'a').close()

def classificar_mensagem(mensagem):
    elogios = ["bom", "ótimo", "excelente", "incrível", "explendido"]
    reclamacoes = ["ruim", "péssimo", "terrível", "horrível"]
    palavras_improprias = ["palavra_impropria1", "palavra_impropria2", "palavra_impropria3"]

    mensagem = mensagem.lower()
    palavras = mensagem.split()

    for palavra in palavras:
        for elogio in elogios:
            if elogio in palavra or palavra in elogio:
                return "elogio"
        for reclamacao in reclamacoes:
            if reclamacao in palavra or palavra in reclamacao:
                return "reclamacao"
        for palavra_impropria in palavras_improprias:
            if palavra_impropria in palavra or palavra in palavra_impropria:
                return "palavras_improprias"
    return None

def registrar_mensagem(tipo, nome, email, mensagem):
    if tipo == "elogio":
        arquivo = "elogios.txt"
    elif tipo == "reclamacao":
        arquivo = "reclamacoes.txt"
    elif tipo == "palavras_improprias":
        arquivo = "palavras_improprias.txt"
    else:
        return

    with open(arquivo, "a") as f:
        f.write(f"Nome: {nome} - Email: {email} - Mensagem: {mensagem}\n")



    
        
        while True:
            mensagem = input("Digite sua mensagem ou 'sair' para encerrar: ")
            if mensagem.lower() == 'sair':
                print("Cadastro encerrado.")
                return

            tipo = classificar_mensagem(mensagem)
            if tipo:
                registrar_mensagem(tipo, nome, email, mensagem)
                print("Mensagem classificada como:", tipo)
            else:
                print("Mensagem não classificada.")

if __name__ == "__main__":
