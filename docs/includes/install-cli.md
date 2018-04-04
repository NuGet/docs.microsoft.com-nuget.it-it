#### <a name="windows"></a>WINDOWS
1. Visitare [nuget.org/downloads](https://nuget.org/downloads) e selezionare NuGet 3.3 o versioni successive (non è compatibile con Mono 2.8.6). La versione più recente è sempre consigliata e 4.1.0+ è necessario pubblicare i pacchetti in nuget.org.
2. Ogni download di `nuget.exe` file direttamente. Indicare il browser per salvare il file in una cartella di propria scelta. Il file è *non* un programma di installazione; non verrà visualizzato alcun elemento se viene eseguito direttamente dal browser.
3. Aggiungere la cartella in cui è stata inserita `nuget.exe` per la variabile di ambiente PATH per utilizzare lo strumento CLI da qualsiasi posizione.

#### <a name="macoslinux"></a>macOS/Linux
I comportamenti possono variare leggermente tramite la distribuzione del sistema operativo.

1. Installare [Mono 4.4.2 o in un secondo momento](http://www.mono-project.com/docs/getting-started/install/).
2. Eseguire i comandi seguenti al prompt dei comandi della shell:
    
    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    # Give the file permissions to execute
    sudo chmod 755 /usr/local/bin/nuget.exe
    ```
3. Creare un alias aggiungendo il seguente script per il file appropriato per il sistema operativo (in genere `~/.bash_aliases` o `~/.bash_profile`):
    
    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```
4. Ricaricare la shell.  Test dell'installazione immettendo `nuget` senza parametri. Guida di NuGet CLI deve essere visualizzato.