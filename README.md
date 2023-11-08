Projeto de Integração de Bancos de Dados - Relacional (SQLAlchemy) e NoSQL (Pymongo)
Este é um projeto prático que demonstra a integração de bancos de dados relacional (SQLite com SQLAlchemy) e NoSQL (MongoDB com Pymongo) usando o ambiente do Google Colab. O projeto foi dividido em duas partes:

Parte 1 - Implementando um Banco de Dados Relacional com SQLAlchemy
Objetivo
Nesta etapa do projeto, configuramos um banco de dados relacional usando o SQLAlchemy. Criamos um esquema com tabelas representando clientes e contas, com a capacidade de realizar operações de inserção e recuperação de dados.

Passos realizados
Configuração do ambiente: Importamos as bibliotecas necessárias e configuramos o ambiente no Google Colab.
python
Copy code
!pip install sqlalchemy
from sqlalchemy import create_engine, Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker
Conexão ao banco de dados: Criamos uma conexão ao banco de dados SQLite.
python
Copy code
engine = create_engine('sqlite:///minhabasededados.db')
Definição das tabelas: Definimos classes para as tabelas do banco de dados usando SQLAlchemy, no caso, as tabelas de Cliente e Conta. Campos adicionais podem ser facilmente adicionados.
python
Copy code
Base = declarative_base()

class Cliente(Base):
    __tablename__ = 'clientes'
    id = Column(Integer, primary_key=True)
    nome = Column(String)
    # Adicione mais campos conforme necessário

class Conta(Base):
    __tablename__ = 'contas'
    id = Column(Integer, primary_key=True)
    cliente_id = Column(Integer)
    saldo = Column(Integer)
    # Adicione mais campos conforme necessário
Criação das tabelas: Criamos as tabelas no banco de dados usando a função create_all.
python
Copy code
Base.metadata.create_all(engine)
Criação de sessão: Criamos uma sessão para interagir com o banco de dados.
python
Copy code
Session = sessionmaker(bind=engine)
session = Session()
Parte 2 - Implementando um Banco de Dados NoSQL com Pymongo
Objetivo
Nesta etapa, configuramos um banco de dados NoSQL MongoDB usando o Pymongo. Criamos uma coleção para clientes e inserimos documentos que agregam informações do modelo relacional.

Passos realizados
Configuração do ambiente: Importamos a biblioteca Pymongo para interagir com o MongoDB.
python
Copy code
import pymongo
Conexão ao banco de dados: Conectamos ao MongoDB (MongoDB Atlas ou instância local).
python
Copy code
client = pymongo.MongoClient("mongodb+srv://<sua_conexao_aqui>")
db = client["banco_de_dados"]
Definição da coleção: Definimos uma coleção chamada "clientes" para armazenar documentos.
python
Copy code
colecao_clientes = db["clientes"]
Inserção de documentos: Inserimos documentos na coleção que refletem informações de clientes e suas contas.
python
Copy code
documento_cliente = {
    "nome": "Nome do Cliente",
    "contas": [
        {"tipo": "Conta Corrente", "saldo": 1000},
        {"tipo": "Conta Poupança", "saldo": 500}
    ]
}
colecao_clientes.insert_one(documento_cliente)
Recuperação de informações: Demonstramos como recuperar informações de documentos usando consultas.
python
Copy code
cliente = colecao_clientes.find_one({"nome": "Nome do Cliente"})
print(cliente)
Como executar o projeto
Para executar este projeto em seu ambiente, siga os passos no Google Colab:

Abra o Google Colab (https://colab.research.google.com/).
Crie um novo notebook ou use um notebook existente.
Copie e cole os blocos de código correspondentes a cada parte do projeto nos blocos de código do seu notebook.
Execute os blocos de código no notebook para configurar e interagir com os bancos de dados.
