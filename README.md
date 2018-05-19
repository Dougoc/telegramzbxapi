#telegramzbxapi

# -*- coding: utf-8 -*-

from zabbix_api import ZabbixAPI

zabbix_server = "http://monitoramento.hu.corp/zabbix" #Endereço ou IP ou FQDN do servidor do Zabbix.
username = "admin" #Informe usuário para acessar. Usuário com perfil de administrador do Zabbix, não necessáriamente o 'admin' padrão.
password = "zabbix" #Senha

#Instanciando a API
conexao = ZabbixAPI(server = zabbix_server, log_level=6)
conexao.login(username, password)

versao = conexao.api_version()
v = "Versao do Zabbix: " + versao

hosts = conexao.host.get({"output": ["hostid", "name"]})

from telegram.ext import Updater
updater = Updater(token='589034099:AAHSZFX9-Nj6BnWTUrohvSlksFjhF8zI5lY')

dispatcher = updater.dispatcher

import logging
logging.basicConfig(format='%(asctime)s - %(name)s - %(levelname)s - %(message)s', level=logging.INFO)

def start(bot, update):
     bot.send_message(chat_id=update.message.chat_id, text="Bem vindo ao bot de acesso ao Zabbix HU:")

from telegram.ext import CommandHandler
start_handler = CommandHandler('start', start)
dispatcher.add_handler(start_handler)

updater.start_polling()

def versao(bot, update):
        bot.send_message(chat_id=update.message.chat_id, text=v)
support_handler = CommandHandler('versao', versao)
dispatcher.add_handler(support_handler)

def host(bot, update):
        bot.send_message(chat_id=update.message.chat_id, text=hosts)
suport_handler = CommandHandler('host', host)
dispatcher.add_handler(support_handler)
