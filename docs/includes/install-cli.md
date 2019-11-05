---
ms.openlocfilehash: 5197447531288a8b071354dbeb3a3ae02f7cce09
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610519"
---
#### <a name="windows"></a>WINDOWS

> [!Note]
> Per l'esecuzione di NuGet.exe 5.0 e versioni successive è richiesto .NET Framework 4.7.2 o versione successiva.

1. Visitare [nuget.org/downloads](https://nuget.org/downloads) e selezionare NuGet 3.3 o versioni successive (la versione 2.8.6 non è compatibile con Mono). È sempre consigliata la versione più recente e la versione 4.1.0+ è obbligatoria per pubblicare i pacchetti in nuget.org.
1. Ogni download è direttamente il file `nuget.exe`. Indicare al browser di salvare il file in una cartella di propria scelta. Il file *non* è un programma di installazione. Non verrà visualizzato alcun elemento se lo si esegue direttamente dal browser.
1. Aggiungere la cartella in cui è stato posizionato il file `nuget.exe` alla variabile di ambiente PATH per usare lo strumento dell'interfaccia della riga di comando da qualsiasi posizione.

#### <a name="macoslinux"></a>macOS/Linux

I comportamenti possono variare leggermente in base alla distribuzione del sistema operativo.

1. Installare [Mono 4.4.2 o versioni successive](https://www.mono-project.com/docs/getting-started/install/).

1. Eseguire il comando seguente da un prompt della shell:

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. Creare un alias aggiungendo lo script seguente al file appropriato per il sistema operativo (in genere `~/.bash_aliases` o `~/.bash_profile`):

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. Ricaricare la shell.  Testare l'installazione immettendo `nuget` senza parametri. Dovrebbe essere visualizzata la Guida dell'interfaccia della riga di comando di NuGet.
