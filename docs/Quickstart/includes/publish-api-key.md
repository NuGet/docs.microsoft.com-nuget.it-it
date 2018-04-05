1. [Accedere all'account personale di nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) o creare un account, se non è già disponibile.

1. Selezionare il nome utente (in alto a destra) e quindi selezionare **API Keys** (Chiavi API).

1. Selezionare **Create** (Crea), specificare un nome per la chiave, selezionare **Select Scopes > Push** (Seleziona ambiti > Push). In **API Key** (Chiave API), immettere * per **Glob pattern** (Criterio GLOB) e quindi selezionare **Create** (Crea). (Vedere di seguito per altre informazioni sugli ambiti.)

1. Dopo avere creato la chiave, selezionare **Copia** per recuperare la chiave di accesso necessaria nell'interfaccia della riga di comando:

    ![Copia della chiave API negli Appunti](../media/QS_Create-02-APIKey.png)

1. **Importante**: salvare la chiave in un luogo sicuro, perché non è possibile copiare la chiave nuovamente in seguito. Se si torna alla pagina della chiave API, è necessario rigenerarla per copiarla. È anche possibile rimuovere la chiave API se non si vuole più eseguire il push tramite l'interfaccia della riga di comando.

L'assegnazione degli ambiti consente di creare chiavi API separate per scopi diversi. Per ogni chiave esiste un intervallo di tempo di scadenza ed è possibile specificare un ambito limitato a pacchetti (o criteri GLOB) specifici. L'ambito per ogni chiave può essere anche limitato a operazioni specifiche: push di nuovi pacchetti e aggiornamenti, push solo degli aggiornamenti o rimozione dall'elenco. Tramite l'assegnazione di un ambito, è possibile creare chiavi API per i diversi utenti che gestiscono i pacchetti per l'organizzazione in modo che abbiamo solo le autorizzazioni necessarie. Per altre informazioni, vedere [Introducing scoped API keys](https://blog.nuget.org/20170202/introducing-scoped-api-keys.html) (Introduzione alle chiavi API con ambito) (blogs.nuget.org).