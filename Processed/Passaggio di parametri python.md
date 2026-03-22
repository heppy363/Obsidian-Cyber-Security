---
tipo: nota_lezione
corso: "Dashboard Python"
tags: [progetto, linguaggiProg, python, uni, programmazione, Completed]
creato: 2026-03-21 14:57
---

# 📝 Lezione: Passaggio di parametri python 
**Corso:** [[Dashboard Python]]

---
## Contenuto
## 1. Il Concetto Cardine: Nomi vs Scatole
Per capire il passaggio dei parametri, devi visualizzare le variabili non come "scatole" che contengono dati, ma come **etichette (nomi)** attaccate a **oggetti** che fluttuano nell'Heap.
Quando passi un argomento a una funzione:
1. Viene creato un nuovo riferimento locale (il parametro della funzione).
2. Questo nuovo riferimento punta allo **stesso identico oggetto** a cui punta la variabile esterna.

## 2. Il Comportamento Differenziato
Il modo in cui la funzione "sembra" comportarsi dipende esclusivamente dalla **mutabilità** dell'oggetto passato.
## Caso A: Oggetti Immutabili (int, float, str, tuple)
Se passi un intero e provi a modificarlo dentro la funzione, Python non modifica l'oggetto originale (che è immutabile). Invece, crea un **nuovo oggetto** e sposta l'etichetta locale su di esso.


```
def modifica(x):
    x = x + 10  # 'x' ora punta a un nuovo oggetto 15. L'oggetto 5 non cambia.
    print(f"Dentro: {x}")

valore = 5
modifica(valore)
print(f"Fuori: {valore}")  # Stamperà ancora 5
```

## Caso B: Oggetti Mutabili (list, dict, set)
Se passi una lista, il riferimento locale punta alla stessa lista in memoria. Poiché le liste sono mutabili, le modifiche effettuate all'interno si riflettono all'esterno.


```
def aggiungi_elemento(lista_locale):
    lista_locale.append(4)  # Modifica l'oggetto esistente in situ

mia_lista = [1, 2, 3]
aggiungi_elemento(mia_lista)
print(mia_lista)  # Stamperà [1, 2, 3, 4]
```

## 3. L'Inganno del Riallocamento
C'è un dettaglio tecnico cruciale: se all'interno della funzione **riassegni** completamente la variabile mutabile, rompi il legame con l'oggetto originale.


```
def riassegna(lista_locale):
    lista_locale = [10, 20]  # Ora lista_locale punta a un NUOVO oggetto

mia_lista = [1, 2, 3]
riassegna(mia_lista)
print(mia_lista)  # Stamperà ancora [1, 2, 3]
```

In questo caso, hai sovrascritto il riferimento locale, non il contenuto dell'oggetto originale.

## 4. Implicazioni nel Design del Software
A livello universitario, questo comportamento impone due regole d'oro:
1. **Evitare i "Default Mutable Arguments":** Mai usare `def func(a=[])`. Poiché la lista viene creata una sola volta al momento della definizione della funzione, le chiamate successive condivideranno la stessa lista, portando a effetti collaterali persistenti.
2. **Chiarezza sugli Side-Effects:** Documentare sempre se una funzione modifica l'oggetto in input o se ne restituisce una copia trasformata.

---
## Collegamenti
- Torna al corso: [[Dashboard Python]]