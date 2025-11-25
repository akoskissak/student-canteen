# Sistem za Rezervaciju Obroka u Menzama

## Cilj Projekta

Sistem je razvijen da digitalizuje proces rezervacija u studentskim menzama. Omogućava studentima da unapred rezervišu termin (slot) za obrok (doručak, ručak ili večeru) u željenoj menzi. Glavni cilj je smanjenje gužvi i vremena čekanja, optimizacija kapaciteta menzi i poboljšanje studentskog iskustva.

---

## Tehnička Arhitektura

Aplikacija je izgrađena kao brzi i skalabilni **API servis** (Backend) koristeći Python. Koristi se troslojna arhitektura sa striktnom separacijom briga.

| Sloj | Tehnologije | Uloga |
| :--- | :--- | :--- |
| **API/Ruter** | FastAPI | Rukovanje HTTP zahtevima, validacija ulaza i pozivanje poslovne logike. |
| **Servisni Sloj** | Python | Sadrži ključnu poslovnu logiku, validacije (datum, vreme, preklapanje) i proračun kapaciteta. |
| **Domen/Entiteti** | Pydantic | Modeliranje podataka (`Canteen` `Reservation` , `Student`) |
| **Repozitorijum** | Python | Abstrahovani sloj za pristup podacima. Koristi se In-Memory skladište (Python rečnici) za simulaciju baze. |

---

## Tehnologije i Verzije

| Tehnologija | Namena | Preporučena Verzija |
| :--- | :--- | :--- |
| **Python** | Programski jezik | 3.12.2 |
| **FastAPI** | ASGI web framework | 0.122.0 |
| **Uvicorn** | ASGI server za pokretanje | 0.38.0 |
| **Pydantic** | Modeliranje podataka i validacija | 2.12.4 |
**Pytest** | Framework za testiranje | 9.0.1

---

## Instrukcije za Podešavanje Okruženja

### 1. Kloniranje Repozitorijuma

```bash
git clone https://github.com/akoskissak/student-canteen
cd student-canteen
```

### 2. Kreiranje i Aktivacija Virtuelnog Okruženja (venv)

```bash
# Kreiranje virtuelnog okruženja
python -m venv venv

# Aktivacija (Windows)
.\venv\Scripts\activate

# Aktivacija (Linux/macOS)
source venv/bin/activate
```

### 3. Instalacija Zavisnosti

```bash
pip install -r requirements.txt
```

## Build Instrukcije

Ovaj projekat ne zahteva klasičan build korak, jer je pisan u Pythonu. Sam build je ekvivalentan instalaciji zavisnosti.

## Pokretanje Aplikacije (Development Mode)
Aplikacija se pokreće korišćenjem ASGI servera, Uvicorn-a.

```bash
# Uverite se da ste u aktivnom virtuelnom okruženju
# Pokretanje aplikacije na portu 8080. Aplikacija se nalazi u modulu main:app
uvicorn main:app --reload --port 8080
```

Aplikacija je dostupna na `http://localhost:8080`

## Instrukcije za Pokretanje Testova

Integracioni testovi nalaze se u fajlu tests/test_integration.py. Trenutno je implementirano 12 integracionih testova.

```bash
# Pokreće testove u fajlu test_integration.py
pytest tests/test_integration.py
