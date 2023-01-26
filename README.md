# Cadastro_Cliente
Código em Python para cadastrar cliente em um banco de dados MySQL

from datetime import date
import mysql.connector
import requests

nome = input("Nome: ")
endereco = input("Cep: ")
telefone = input("Telefone: ")
email =  input("E-mail: ")
cpf = input("CPF: ")
data = str(date.today())

dados = nome + "','" + endereco + "'," + telefone + ",'" + email + "'," + cpf + "," + data + ')'
declaracao = """insert into cliente
(nome, endereco, telefone, email, cpf, data)
values ('"""
sql = declaracao + dados
print(sql)
try:
    conexao = mysql.connector.connect(host="localhost", user="root", passwd="huyner93auany03", database="bd")
    
    cadastrar_cliente = sql
    cursor = conexao.cursor()
    cursor.execute(cadastrar_cliente)
    conexao.commit()
    print(cursor.rowcount, "Cliente Inserido com Sucesso!")
    cursor.close()
except mysql.connector.Error as erro:
    print(f"Falha ao inserir dados na tabela! {erro}")
finally:
    if (conexao.is_connected()):
        cursor.close()
        print("Conexão ao MySQL finalizada!")

