Criação ambiente virtual
```shell
python3 -m venv .
```

Entrando no ambiente virtual
```shell
source bin/activate
```

Instalando a lib do bot telegram
```shell
pip install python-telegram-bot
```

Código bot simples
```python
from typing import Final

from telegram import Update

from telegram.ext import Application, CommandHandler, MessageHandler, filters, ContextTypes

TOKEN: Final = '$BOT_TOKEN$'

BOT_USERNAME: Final = '$BOT_USERNAME'

# Commands
async def start_command(update: Update, context: ContextTypes.DEFAULT_TYPE):
	await update.message.reply_text('Hello! I am a delivery bot')

async def help_command(update: Update, context: ContextTypes.DEFAULT_TYPE):
	await update.message.reply_text('I am a delivery bot!')

async def custom_command(update: Update, context: ContextTypes.DEFAULT_TYPE):
	await update.message.reply_text('I am a custom command')

# Responses
def handle_response(text: str) -> str:
	processed: str = text.lower()
	
	if 'hello' in processed:
		return 'Hey There!'
	
	if 'how are you' in processed:
		return 'I am fine, thank you!'
	
	if 'I love python' in processed:
		return 'I love python too!'
		
	return 'I do not understand what you wrote'

  

async def handle_message(update: Update, context: ContextTypes.DEFAULT_TYPE):

	text: str = update.message.text
	
	print(f'User ({update.message.chat.id}) sent: {text}')
	
	response: str = handle_response(text)
	
	print(f'Response: {response}')
	  
	await update.message.reply_text(response)

async def error(update: Update, context: ContextTypes.DEFAULT_TYPE):
	print(f'Update {update} caused error {context.error}')

  

if __name__ == '__main__':
	print('Bot is running!')
	
	app = Application.builder().token(TOKEN).build()
	
	# Comando handlers
	app.add_handler(CommandHandler('start', start_command))
	app.add_handler(CommandHandler('help', help_command))
	app.add_handler(CommandHandler('custom', custom_command))
	
	# Mensagem handler para qualquer texto
	app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, handle_message))
	
	# Handler de erros
	app.add_error_handler(error)
	
	print('Bot is polling!')
	
	app.run_polling(poll_interval=3)
```

Para rodar
```shell
python3 main.py
```