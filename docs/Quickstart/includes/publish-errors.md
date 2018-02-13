Gli errori dal comando `push` indicano in genere il problema. Ad esempio, è possibile avere dimenticato di aggiornare il numero di versione nel progetto e quindi tentare di pubblicare un pacchetto già esistente.

È anche possibile che vengano visualizzati errori quando si tenta di pubblicare un pacchetto usando un identificatore già esistente nell'host. Il nome "AppLogger", ad esempio, esiste già. In tal caso, il comando `push` genera l'errore seguente:

```output
Response status code does not indicate success: 403 (The specified API key is invalid, has expired, or does not have permission to access the specified package.).
```

Se si usa una chiave API valida appena creata, questo messaggio indica un conflitto di denominazione, condizione non completamente chiara nella parte dell'errore relativa alle autorizzazioni. Modificare l'identificatore del pacchetto, ricompilare il progetto, ricreare il file `.nupkg` e quindi ripetere il comando `push`.