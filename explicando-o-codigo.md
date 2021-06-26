# Explicação dos códigos

Nesse arquivo vou deixar as linhas comentadas do passo a passo de cada linha<br>
No arquivo <a href="">readme.md</a> vou deixar os problemas/ erros que encontrei durante o processo

# Arquivo main.py

//Eu utilizei o Visutal Studio(VS) para criar o código

//primeiro vamos baixar o python no VS, npm install python
//após a instalação do python vamos baixar as bibliotecas
// pip install SpeechRecognition 
// pip install pyaudio
// pip install requests 
// pip install webbrowser 
// pip install pyttsx3
// pip install config 
// pip install random

// agora que instalamos as bibliotecas vamos importar as bibliotecas conforme abaixo

import speech_recognition as sr
import pyttsx3
from config import *
from random import choice

// vamos iniciar o pyttsx3 para que possa reproduzir

reproducao = pyttsx3.init()

def sai_som(reposta):
	reproducao.say(reposta)
	reproducao.runAndWait()

def assistente():
	print("Oi, qual  é o seu nome completo")
	sai_som("Oi, qual é o seu nome completo")
	while True:
		resposta_erro_aleatoria = choice(lista_erros)
		#rec = sr.Recognizer()

		#with sr.Microphone() as s:
			#rec.adjust_for_ambient_noise(s)

		while True:
			try:
				#audio = rec.listen(s)
				user_name = input("")
				user_name = verifica_nome(user_name)
				name_list()
				apresentacao = "{}".format(verifica_nome_exist(user_name))
				print(apresentacao)
				sai_som(apresentacao)
		
				brute_user_name = user_name
				user_name = user_name.split(" ")
				user_name = user_name[0]
				break
			except sr.UnknownValueError:
				sai_som(resposta_erro_aleatoria)
		break


	print("="* len(apresentacao))
	print("Ouvindo...")

	while True:
		resposta_erro_aleatoria = choice(lista_erros)
		#rec = sr.Recognizer()

		#with sr.Microphone() as s:
			#rec.adjust_for_ambient_noise(s)

		while True:
			try:
				# audio = rec.listen(s)
				entrada = input("")
				print("{}: {}".format(user_name, entrada))

				# Abri links no navegador
				if "abrir" in entrada:
					reposta = abrir(entrada)

				# Operações matemáticas
				elif "quanto é" in entrada:

					entrada = entrada.replace("quanto é", "")
					reposta = calcula(entrada)
				# Pede tempo
				elif "qual a temperatura" in entrada:

					lista_tempo = temperatura()
					temp = lista_tempo[0]
					temp_max = lista_tempo[1]
					temp_min = lista_tempo[2]

					reposta = "A temperatura de hoje é {:.2f}º. Temos uma máxima de {:.2f}º e uma minima de {:.2f}º".format(temp, temp_max, temp_min)

				# Informações da cidade
				elif "informações" in entrada and "cidade" in entrada:

					reposta = "Mostrando informações da cidade"
				else:
					reposta = conversas[entrada]

				if reposta == "Mostrando informações da cidade":
					#mostra informações da cidade

					lista_infos = clima_tempo()
					longitude = lista_infos[0]
					latitude = lista_infos[1]
					temp = lista_infos[2]
					pressao_atm = lista_infos[3]
					humidade = lista_infos[4]
					temp_max = lista_infos[5]
					temp_min = lista_infos[6]
					v_speed = lista_infos[7]
					v_direc = lista_infos[8]
					nebulosidade = lista_infos[9]
					id_da_cidade = lista_infos[10]

					print("Assistente:")
					print("Mostrando informações de {}\n\n".format(cidade))
					sai_som("Mostrando informações de {}".format(cidade))
					print("Longitude: {}, Latitude: {}\nId: {}\n".format(longitude, latitude, id_da_cidade))
					print("Temperatura: {:.2f}º".format(temp))
					print("Temperatura máxima: {:.2f}º".format(temp_max))
					print("Temperatura minima: {:.2f}º".format(temp_min))
					print("Humidade: {}".format(humidade))
					print("Nebulosidade: {}".format(nebulosidade))
					print("Velocidade do vento: {}m/s\nDireção do vento: {}".format(v_speed,v_direc))

				else:
					print("Assistente: {}".format(reposta))
					sai_som("{}".format(reposta))

			except sr.UnknownValueError:
				sai_som(resposta_erro_aleatoria)
			except KeyError:
				pass


if __name__ == '__main__':
	intro()
	sai_som("Iniciando")
	assistente()


____________________________________________________________________________
# Arquivo config.py
import requests as rq
import webbrowser as web 


version = "1.5.0"
cidade = 'joinville'
caminho_navegador = "C:/Program Files/Vivaldi/Application/vivaldi.exe %s"

def intro():
	msg = "Assistente - version {} / by: Fulano beltrano ciclano".format(version)
	print("-" * len(msg) +  "\n{}\n".format(msg)  +   "-" * len(msg))


lista_erros = [
		"Não entendi nada",
		"Desculpe, não entendi",
		"Repita novamente por favor"
]

conversas = {
	"Olá": "oi, tudo bem?",
	"sim e você": "Estou bem obrigada por perguntar",
}

comandos = {
	"desligar": "desligando",
	"reiniciar": "reiniciando"
}


def verifica_nome(user_name):
	if user_name.startswith("Meu nome é"):
		user_name = user_name.replace("Meu nome é", "")
	if user_name.startswith("Eu me chamo"):
		user_name = user_name.replace("Eu me chamo", "")
	if user_name.startswith("Eu sou o"):
		user_name = user_name.replace("Eu sou o", "")
	if user_name.startswith("Eu sou a"):
		user_name = user_name.replace("Eu sou a", "")

	return user_name 


def  verifica_nome_exist(nome):
	dados = open("dados/nomes.txt", "r")
	nome_list = dados.readlines()

	if not nome_list:
		vazio = open("dados/nomes.txt", "r")
		conteudo = vazio.readlines()
		conteudo.append("{}".format(nome))
		vazio = open("dados/nomes.txt", "w")
		vazio.writelines(conteudo)
		vazio.close()

		return "Olá {}, prazer em te conhecer!".format(nome)

	for linha in nome_list:
		if linha == nome:
			return "Olá {}, acho que já nos conhecemos".format(nome)

	vazio = open("dados/nomes.txt", "r")
	conteudo = vazio.readlines()
	conteudo.append("\n{}".format(nome))
	vazio = open("dados/nomes.txt", "w")
	vazio.writelines(conteudo)
	vazio.close()

	return "Oi {} é a primeira vez que nos falamos".format(nome)


def name_list():
	try:
		nomes = open("dados/nomes.txt", "r")
		nomes.close()

	except FileNotFoundError:
		nomes = open("dados/nomes.txt", "w")
		nomes.close()


def calcula(entrada):
	if "mais" in entrada or "+" in entrada:
		# É soma
		entradas_recebidas = entrada.split(" ")
		resultado = int(entradas_recebidas[1]) + int(entradas_recebidas[3])

	elif "menos" in entrada or "-" in entrada:
		# É subtração

		entradas_recebidas = entrada.split(" ")
		resultado = int(entradas_recebidas[1]) - int(entradas_recebidas[3])

	elif "vezes" in entrada or "x" in entrada:
		# É vezes

		entradas_recebidas = entrada.split(" ")
		resultado = round(float(entradas_recebidas[1]) * float(entradas_recebidas[3]), 2)

	elif "dividido" in entrada or "/" in entrada:
		# É divisão

		entradas_recebidas = entrada.split(" ")
		resultado = round(float(entradas_recebidas[1]) / float(entradas_recebidas[4]), 2)

	else:

		resultado = "Operação não encontrada"


	return resultado



def clima_tempo():	
	endereco_api = "http://api.openweathermap.org/data/2.5/weather?appid=9e1280f88eef9db700e867bb898fd3ec&q="
	url = endereco_api + cidade

	infos = rq.get(url).json()


	# Coord
	longitude = infos['coord']['lon']
	latitude = infos['coord']['lat']
	# main
	temp = infos['main']['temp'] - 273.15 # Kelvin para Celsius
	pressao_atm = infos['main']['pressure'] / 1013.25 #Libras para ATM
	humidade = infos['main']['humidity'] # Recebe em porcentagem
	temp_max= infos['main']['temp_max'] - 273.15 # Kelvin para Celsius
	temp_min = infos['main']['temp_min'] - 273.15 # Kelvin para Celsius

	#vento
	v_speed = infos['wind']['speed'] # km/ h
	v_direc = infos['wind']['deg'] #Recebe em graus

	#clouds / nuvens

	nebulosidade = infos['clouds']['all']

	#id
	id_da_cidade = infos['id']

	# 11
	return [longitude, latitude, 
		temp, pressao_atm, humidade, 
		temp_max, temp_min, v_speed, 
		v_direc, nebulosidade, id_da_cidade]


def temperatura():
	temp_atual = clima_tempo()[2]
	temp_max = clima_tempo()[5]
	temp_min = clima_tempo()[6]
	
	return [temp_atual, temp_max, temp_min]



def abrir(fala):
	try:
		if "google" in fala:
			web.get(caminho_navegador).open("google.com.br/")
			return "abrindo google"
		elif "facebook" in fala:
			web.get(caminho_navegador).open("facebook.com.br/")
			return "abrindo facebook"
		else:
			return "site não cadastrado para aberturas"
	except:
		return "houve um erro"