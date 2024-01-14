from telegram.ext import Updater, MessageHandler, CallbackContext, Filters
from telegram import Update, User

def risposta_automatica(update: Update, context: CallbackContext) -> None:
    # Verifica se l'utente ha già interagito con il bot
    if 'prima_interazione' not in context.user_data:
        # Memorizza che l'utente ha interagito con il bot
        context.user_data['prima_interazione'] = True
        return

    # Ottieni il nome dell'utente che ha inviato il messaggio
    user: User = update.message.from_user
    nome_utente = user.first_name if user.first_name else "Utente"

    # Messaggio da inviare come risposta automatica con il nome dell'utente
    messaggio = f"Ciao {nome_utente}, questo è un messaggio automatico per ricordare che sono una donna italiana molto riservata " \
                "e ospito solo uomini italiani.\n\nSe vuoi contattarmi per un incontro e vedere foto e video, " \
                "allora entra nel mio canale Telegram: https://t.me/+MhuB_dI0i3YwZDFh\n\n" \
                "Se vuoi prenotare un incontro a casa mia, inviami direttamente un messaggio al mio indirizzo mail personale: " \
                "prenotazionesara@gmail.com\n\nTi rispondo subito... "

    # Invia il messaggio di risposta
    update.message.reply_text(messaggio)

def main():
    # Inizializza il tuo token del bot
    token = '6873056201:AAFIWRb2pg2iyfdodupSBmCD4eVygQaFrkc'

    # Crea un oggetto Updater e passa il token
    updater = Updater(token)

    # Ottieni il dispatcher per registrare i gestori di eventi
    dp = updater.dispatcher

    # Aggiungi un gestore di messaggi con la risposta automatica
    dp.add_handler(MessageHandler(Filters.text & ~Filters.command, risposta_automatica))

    # Avvia il bot
    updater.start_polling()

    # Mantieni il bot in esecuzione finché non viene interrotto
    updater.idle()

if __name__ == '__main__':
    main()
