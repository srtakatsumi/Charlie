# Assistente virtual 

# Introdução

A proposta do projeto de desenvolver um assistente virtual em python<br>
        - Recursos Humanos: Victoria<br>
        - Ferramentas: Noteebok, internet, livros e vídeos.<br>
        - Softwares: IDE (Visual Code Studio)<br>

# Baixando o projeto

- Para baixar o repositório : <b>git clone  <a href=""> </a> </b> <br>
- Abrir o projeto no vscode <br>
- Abra o terminal e digite : 
        - npm install python
        - pip install virtualenv
- Após a instalação do python vamos baixar as bibliotecas<br>
        - pip install SpeechRecognition
        - pip install PyAudio
        - pip install requests 
        - pip install webbrowser 
        - pip install pyttsx3
        - pip install config 
        - pip install random

- Para iniciar a aplicação: <b> python main.py </b> <br>


# Objetivo 
Fazer o assistente responder perguntas simples como perguntar <br>
- se está bem;<br>
- perguntar seu nome;<br>
- Informar a temperatura;<br>
- calculadora simples

# Interagindo com a Charlie

- Informe seu nome assim que ela perguntar;
- Diga Oi ou Olá
- Responda Sim ou Não;
- Para calcular pergunte "quanto é " e informe os valores

# Bibliotecas

- SpeechRecognition
- pyaudio
- requests 
- webbrowser 
- pyttsx3
- config 
- random


# Extra 

O virtualenv cria ambientes em Python isolados.<br>

# Erros no código e soluções

Vou deixar aqui os problemas/ erros que encontrei durante o desenvolvimento e como resolvi. 

Problem: import "speech_recognition" could not be resolved Pylance(reportMissingImports) [1,8] <br>
Solution: pip3 install speechrecognition <br>

Problem: import "pyttsx3" could not be resolved Pylance(reportMissingImports) [2,8]<br>
Solution:pip install pyttsx3 <br>

roblem: import "requests" could not be resolved Pylance(reportMissingImports) [3,8] <br>
Solution: pip3 install requests<br>

Problem: FileNotFoundError: [Errno 2] No such file or directory: 'dados/nomes.txt' <br>
Solution: Havia esquecido de criar a pasta dados<br>

Problem: Charlie não está ouvindo<br>
Solution:<br>
