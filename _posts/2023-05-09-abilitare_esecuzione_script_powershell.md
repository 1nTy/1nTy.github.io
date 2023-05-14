---
title: Abilitare l'esecuzione degli script PowerShell
date: 2023-05-09 18:05:00 +0800
categories: [Windows,PowerShell]
tags: [windows,powershell]
math: true
---

Se siete qua è perché avete ricevuto un messaggio simile a questo all'esecuzione di uno script **PowerShell**:

```
L'esecuzione di script è disabilitata nel sistema in uso.
Per ulteriori informazioni, vedere about_Execution_Policies all'indirizzo
https://go.microsoft.com/fwlink/?LinkID=135170.
```

Per eseguire gli script **PowerShell**, infatti, è necessario che la loro esecuzione sia permessa.

Vediamo quindi come verificare l'attuale *policy* applicata, quali sono le opzioni possibili e come modificarla (globalmente o per utente).

## Verifica della policy attuale

Per verificare la *policy* applicata applicata all'utente è sufficiente aprire una finestra **PowerShell** e digitare

```powershell
Get-ExecutionPolicy
```
che restituirà una delle seguenti voci

|     Policy     |                 Esecuzione                 | Descrizione                                                  |
| :------------- | :----------------------------------------: | :----------------------------------------------------------- |
|  `Restricted`  |      <font color=red>$\times$</font>       | disabilitato                                                 |
| `RemoteSigned` | <font color=DarkOrange>$\checkmark$</font> | solo script creati in locale o firmati da un editor attendibile |
|  `AllSigned`   | <font color=DarkOrange>$\checkmark$</font> | solo script firmati da un editor attendibile creati da un editor attendibile |
| `Unrestriced`  |   <font color=green>$\checkmark$</font>    | esecuzione permessa in ogni caso                             |


>`RemoteSigned` permette una certa flessibilità senza eccessive limitazioni e con rischi moderati per la sicurezza
{: .prompt-tip }

>`Unrestricted` è un possible rischio per la sicurezza, abilitalo solo temporaneamente e preferibilmente al solo livello utente
{: .prompt-danger }


## Modifica della policy

> Sostituisci `%policy_name%` con la *policy* desiderata fra quelle sopra citate
{: .prompt-info }

Per modificare la *policy* è sufficiente aprire **PowerShell** e digitare

### Modifica a livello utente

```powershell
Set-ExecutionPolicy -Scope CurrentUser %policy_name%
```

### Modifica a livello globale

```powershell
Set-ExecutionPolicy %policy_name%
```

>Per cambiare la *policy* a livello globale **PowerShell** deve essere eseguito come amministratore
{: .prompt-warning }
