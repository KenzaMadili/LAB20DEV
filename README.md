# 📒 NumberBook — Lab Android


https://github.com/user-attachments/assets/ef4a61e2-bc42-447a-93b0-52b657bebbf1


Application Android de gestion de contacts connectée à une API REST PHP/MySQL.

---


## 🧱 Stack technique

| Couche | Technologie |
|--------|-------------|
| Mobile | Android (Java) |
| Backend | PHP (architecture MVC légère) |
| Base de données | MySQL via XAMPP |
| Communication | HTTP REST + JSON |
| UI | Material Design 3 (dark theme) |

---

## 📁 Structure du projet

### Backend — `NUMBERBOOK-API/`
```
NUMBERBOOK-API/
├── api/
│   ├── getAllContacts.php     # GET — retourne tous les contacts
│   ├── insertContact.php     # POST — insère un nouveau contact
│   └── searchContact.php     # GET — recherche par mot-clé
├── config/
│   └── Database.php          # Connexion PDO à MySQL
├── model/
│   └── Contact.php           # Modèle Contact
└── service/
    └── ContactService.php    # Logique métier (getAll, insert, search)
```

### Frontend Android — `app/`
```
app/src/main/
├── java/com/example/numberbook/
│   ├── MainActivity.java       # Activité principale
│   ├── Contact.java            # Modèle Contact
│   └── ContactAdapter.java     # Adapter RecyclerView
└── res/
    ├── layout/
    │   ├── activity_main.xml   # Layout principal
    │   └── item_contact.xml    # Layout carte contact
    └── drawable/
        ├── bg_avatar.xml       # Fond arrondi avatar
        └── bg_btn_call.xml     # Fond bouton appel
```

---

## ⚙️ Installation & configuration

### 1. Base de données

Ouvrir phpMyAdmin (`http://localhost/phpmyadmin`) et exécuter :

```sql
CREATE DATABASE IF NOT EXISTS numberbook;

USE numberbook;

CREATE TABLE contact (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    phone VARCHAR(20) NOT NULL
);

INSERT INTO contact (name, phone) VALUES
('Amine Khalil', '+212 6 12 34 56 78'),
('Fatima Aziz', '+212 6 98 76 54 32'),
('Youssef Benali', '+212 6 55 44 33 22');
```

### 2. Backend PHP

- Placer le dossier `NUMBERBOOK-API/` dans `C:\xampp\htdocs\`
- Démarrer **Apache** et **MySQL** depuis le panneau XAMPP
- Tester dans le navigateur : `http://localhost/numberbook-api/api/getAllContacts.php`

### 3. Application Android

- Ouvrir le projet dans **Android Studio**
- Modifier l'URL de base dans `MainActivity.java` selon l'environnement :

| Environnement | URL |
|---------------|-----|
| Émulateur | `http://10.0.2.2/numberbook-api/api/` |
| Téléphone réel | `http://192.168.1.XXX/numberbook-api/api/` |

- Lancer l'application via **Run > Run 'app'**

---

## 🌐 Endpoints API

### GET — Récupérer tous les contacts
```
GET /numberbook-api/api/getAllContacts.php
```
Réponse :
```json
[
  { "id": "1", "name": "Amine Khalil", "phone": "+212 6 12 34 56 78" },
  { "id": "2", "name": "Fatima Aziz", "phone": "+212 6 98 76 54 32" }
]
```

### POST — Insérer un contact
```
POST /numberbook-api/api/insertContact.php
Content-Type: application/json
```
Body :
```json
{
  "name": "Nouveau Contact",
  "phone": "+212 6 00 00 00 00"
}
```
Réponse :
```json
{ "success": true, "message": "Contact inséré avec succès" }
```

### GET — Rechercher un contact
```
GET /numberbook-api/api/searchContact.php?keyword=Amine
```

---

## 🎨 Design

- **Thème** : Dark mode élégant
- **Palette** :
  - Fond principal : `#0F0F1A`
  - Surface carte : `#1A1A2E`
  - Accent violet : `#7C3AED`
  - Texte principal : `#E8E4FF`
  - Texte secondaire : `#6B6B85`
- **Composants** : RecyclerView + CardView + ExtendedFloatingActionButton

---

## 🐛 Erreurs fréquentes

| Erreur | Cause | Solution |
|--------|-------|----------|
| `404 Not Found` | URL incomplète | Ajouter `/api/` dans l'URL |
| `Table not found` | Table MySQL inexistante | Exécuter le script SQL |
| `Champs manquants` | Header manquant dans Postman | Ajouter `Content-Type: application/json` |
| `bg_avatar not found` | Drawable manquant | Créer `bg_avatar.xml` dans `res/drawable/` |
| `onCreateViewHolder clashes` | Méthode en double | Supprimer le doublon dans l'adapter |

---

## 👨‍💻 Auteur

MADILI Kenza
