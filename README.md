# Previdenza Smart — Simulatore Riscattabilità 2026

Strumento interattivo per capire se il tuo fondo pensione ti permetterà di **ritirare il 100% in capitale** oppure se sarai obbligato a convertirne una parte in rendita vitalizia.

---

## A cosa serve?

Dal **1° luglio 2026**, la Legge di Bilancio cambia le regole di uscita dai fondi pensione complementari (Art. 11, D.Lgs 252/2005):

- Se la rendita teorica che ricaveresti dal tuo montante è **piccola** (sotto una certa soglia), puoi ritirare **tutto in capitale**: prendi i soldi e vai.
- Se la rendita è **sopra la soglia**, devi convertire **almeno il 40%** del montante in rendita vitalizia (una "pensione" che ti paga il fondo finché vivi). Il restante 60% lo puoi ritirare in capitale.

**Il simulatore ti dice in quale dei due scenari ti trovi**, proiettando la tua situazione attuale nel futuro.

---

## Come funziona il test di legge

Il calcolo si basa su un confronto tra due valori:

### 1. La rendita teorica
Il simulatore prende il tuo montante finale atteso, ne considera il 70%, e lo moltiplica per un **coefficiente di conversione** che dipende dalla tua età e dal tuo sesso al momento del pensionamento.

> **Esempio**: Montante finale € 149.000 × 70% = € 104.300 × coefficiente 3,55% = **€ 3.700/anno**

### 2. La soglia di legge
È pari al **50% dell'Assegno Sociale** (€ 7.101 nel 2026), rivalutato per l'inflazione fino all'anno in cui andrai in pensione.

> **Esempio** con 15 anni al pensionamento e inflazione al 2%: € 7.101 × (1,02)^15 × 50% = **€ 4.779/anno**

### L'esito
- **Rendita teorica < soglia** → ✅ Puoi ritirare tutto in capitale
- **Rendita teorica ≥ soglia** → ⚠️ Obbligo: max 60% capitale, min 40% rendita

---

## Cosa devi inserire

| Campo | Cosa significa | Dove lo trovi |
|---|---|---|
| **Montante Attuale** | Quanto hai già accumulato nel fondo | Ultimo estratto conto del fondo pensione |
| **Anno di Nascita** | Serve per calcolare la tua età al pensionamento | — |
| **Anni al Pensionamento** | Quanti anni mancano al momento in cui uscirai dal fondo | Dipende dalla tua situazione lavorativa |
| **Sesso** | Uomo o donna: influenza il coefficiente di conversione | — |
| **RAL** | Reddito Annuo Lordo: base per calcolare i contributi futuri | Ultima busta paga o CU |
| **Contributo Lavoratore %** | Quota a tuo carico versata al fondo | Contratto collettivo o regolamento fondo |
| **Contributo Datore %** | Quota a carico del datore di lavoro | Contratto collettivo o regolamento fondo |
| **TFR** | Se il TFR viene versato al fondo (≈ 7,41% della RAL) | Dipende dalla tua scelta al momento dell'adesione |
| **Rendimento Netto Fondo** | Quanto rende il tuo comparto di investimento all'anno | Comunicazione periodica del fondo / sito COVIP |
| **Inflazione Attesa** | Quanto cresceranno i prezzi ogni anno (stima) | Il default 2% è il target BCE |

---

## Il coefficiente di conversione: la variabile chiave

Il coefficiente di conversione risponde alla domanda: **per ogni euro di montante, quanti centesimi di rendita annua ricevi?**

Dipende da tre fattori:

- **Età**: più sei vecchio al pensionamento → coefficiente più alto → rendita più alta → più facile superare la soglia
- **Sesso**: le donne vivono mediamente di più → coefficiente più basso → a parità di montante, rendita inferiore → più facile restare sotto soglia
- **Anno di uscita**: la speranza di vita si allunga → i coefficienti futuri saranno più bassi di quelli attuali

### Le due modalità del simulatore

Puoi scegliere tra:

| Modalità | Cosa fa | Quando usarla |
|---|---|---|
| **Coefficienti Statici (2024)** | Usa i coefficienti attuali, come se la speranza di vita non cambiasse mai | Scenario ottimistico: ti mostra il "caso peggiore" per la riscattabilità |
| **Coefficienti Dinamici (proiettati)** | Usa coefficienti che tengono conto dell'allungamento atteso della vita (Tariffa 75A0, proiezioni ISTAT 2024–2060) | Scenario più realistico e prudente |

> **In pratica**: i coefficienti dinamici sono più bassi → producono una rendita teorica inferiore → è più facile restare sotto soglia. Ma nessuno sa con certezza quali saranno i coefficienti tra 15 o 20 anni. Confrontare le due modalità ti dà un'idea dell'intervallo possibile.

---

## Come leggere i risultati

### Il verdetto principale
- **Verde (✅ 100% Capitale Prelevabile)**: con i parametri che hai inserito, potrai ritirare tutto in capitale. Il "margine di sicurezza" ti dice di quanto sei sotto la soglia.
- **Giallo (⚠️ Obbligo Rendita)**: superi la soglia. Il simulatore ti mostra quanto potrai prendere in capitale (max 60%) e quanto dovrai convertire in rendita (min 40%).

### I numeri chiave

| Indicatore | Significato |
|---|---|
| **Montante Finale Atteso (MFA)** | Quanto avrai nel fondo al pensionamento (stima) |
| **Rendita Annuale da 70% MFA** | La rendita teorica calcolata dalla legge per decidere se puoi avere tutto in capitale |
| **Soglia di Legge** | Il valore sotto il quale la rendita deve restare per poter ritirare il 100% |
| **Gap** | Differenza tra soglia e rendita: se positivo sei OK, se negativo sfori |
| **Soglia Limite Montante** | Il montante massimo che puoi avere senza sforare: il numero più importante per pianificare |

### Il grafico
La linea blu è la crescita del tuo montante nel tempo. La linea rossa tratteggiata è la soglia limite: finché la blu sta sotto la rossa, sei al sicuro.

---

## Formule utilizzate

Per chi vuole verificare i calcoli, ecco la logica anno per anno:

**Proiezione del montante** (per ogni anno da 1 a N):
```
Rendimento(t)  = Montante(t-1) × rendimento netto %
Contributo(t)  = RAL(t) × (% lavoratore + % datore)
TFR(t)         = RAL(t) / 13,5
Montante(t)    = Montante(t-1) + Rendimento(t) + Contributo(t) + TFR(t)
RAL(t+1)       = RAL(t) × (1 + crescita salariale %)
```

**Test finale**:
```
Assegno Sociale futuro  = € 7.101,12 × (1 + inflazione)^N
Soglia di legge         = AS futuro × 50%
Rendita teorica         = MFA × 70% × coefficiente di conversione

Se Rendita teorica < Soglia → 100% capitale
Se Rendita teorica ≥ Soglia → max 60% capitale + min 40% rendita
```

**Soglia limite montante** (il numero chiave per pianificare):
```
Montante massimo = Soglia di legge / (70% × coefficiente)
```

---

## Avvertenze importanti

- Questa è una **simulazione indicativa**, non una consulenza finanziaria o previdenziale.
- Il **coefficiente di conversione futuro è incerto**: le tavole vengono aggiornate periodicamente e nessuno può garantire i valori tra 10, 20 o 30 anni.
- Il **rendimento del fondo** è una stima: i mercati finanziari sono volatili e i rendimenti passati non garantiscono quelli futuri.
- I valori in **"termini reali"** mostrano il potere d'acquisto effettivo (al netto dell'inflazione): sono quelli che contano davvero.
- Per situazioni complesse o decisioni importanti, consulta un professionista.

---

## Strategia: più posizioni per restare sotto soglia

Se il tuo montante rischia di superare la soglia limite, una strategia possibile è **aprire più posizioni** in fondi pensione diversi. Ogni posizione viene valutata separatamente: se ciascuna resta sotto la soglia, puoi ritirare il 100% in capitale da ognuna.

---

## Fonti normative

- **D.Lgs 252/2005**, Art. 11, co. 3 — Prestazioni in forma di capitale
- **Legge di Bilancio 2026** — Modifica delle percentuali (dal 1/7/2026: max 60% capitale, min 40% rendita)
- **Assegno Sociale 2026**: € 7.101,12 annui (fonte INPS)
- **Coefficienti di conversione**: Tariffa 75A0, tasso tecnico 0%, tavole di sopravvivenza ISTAT proiezione 2015–2024, orizzonte 2024–2060

---

## Tecnologia

File HTML singolo, completamente client-side. Nessun dato viene inviato a server esterni. Funziona aprendo il file nel browser.

Librerie esterne (via CDN):
- [Tailwind CSS](https://tailwindcss.com/) — layout e stile
- [Chart.js](https://www.chartjs.org/) — grafico di proiezione
- [Font Awesome](https://fontawesome.com/) — icone

---

## Licenza

Questo strumento è rilasciato a scopo educativo e informativo. L'autore non si assume alcuna responsabilità per decisioni prese sulla base dei risultati della simulazione.
