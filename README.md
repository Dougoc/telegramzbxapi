# -*- coding: utf-8 -*-
from zabbix_api import ZabbixAPI

zabbix_server = "http://monitoramento.hu.corp/zabbix" #Endereço ou IP ou FQDN do servidor do Zabbix.
username = "------" #Informe usuário para acessar. Usuário com perfil de administrador do Zabbix, não necessáriamente o 'admin' padrão.
password = "-----" #Senha

#Instanciando a API
conexao = ZabbixAPI(server = zabbix_server, log_level=6)
conexao.login(username, password)

versao = conexao.api_version()

from telegram.ext import Updater
updater = Updater(token='589034099:AAHSZFX9-Nj6BnWTUrohvSlksFjhF8zI5lY')

dispatcher = updater.dispatcher

import logging
logging.basicConfig(format='%(asctime)s - %(name)s - %(levelname)s - %(message)s', level=logging.INFO)

def start(bot, update):
     bot.send_message(chat_id=update.message.chat_id, text="teste")

from telegram.ext import CommandHandler
start_handler = CommandHandler('start', start)
dispatcher.add_handler(start_handler)

updater.start_polling()

def ok(bot, update):
        bot.send_message(chat_id=update.message.chat_id, text="teste1")
        bot.send_chat_action(chat_id=chat_id, action=telegram.ChatAction.TYPING)

support_handler = CommandHandler('ok', ok)
dispatcher.add_handler(support_handler)
