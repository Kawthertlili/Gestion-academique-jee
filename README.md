# Gestion-academique-jee
Application web de **gestion académique** développée en **Jakarta EE** permettant de gérer les **étudiants**, **examens**, **sessions** et **spécialités** via une interface web développée en Jakarta EE avec Servlets, EJB et JPA (MySQL).

## Présentation générale

Ce projet a été réalisé dans le cadre d’un mini-projet JEE.  
Il illustre une architecture 3-tiers classique :

- **Frontend** : JSP + Bootstrap + FontAwesome  
- **Contrôleurs** : Servlets Jakarta (`@WebServlet`)  
- **Métier & persistance** : EJB stateless + JPA (`@Entity`, `@PersistenceContext`)  
- **Base de données** : MySQL (datasource JTA `java:/coursDS`)

L’objectif est d’offrir une interface simple pour :

- Ajouter / modifier / supprimer des **étudiants**
- Gérer les **examens** (matière, durée)
- Gérer les **sessions** d’examen
- Gérer les **spécialités**

##  Fonctionnalités

### Étudiants
- Création d’un étudiant (ID, nom, prénom, email, spécialité)
- Liste des étudiants
- Modification des informations d’un étudiant
- Suppression d’un étudiant

### Examens
- Création d’un examen (ID, matière, durée)
- Liste des examens
- Mise à jour d’un examen
- Suppression d’un examen

### Sessions
- Gestion de sessions d’examen (id, nom, date, examen associé)
- Utilisation d’un `SessionId` embarqué pour lier session / étudiant

### Spécialités
- Gestion des spécialités (id, nom)

### Interface utilisateur
- Page principale : `Home.jsp`
- Navigation par sections (Étudiants, Examens, Sessions, Spécialités)
- Design avec **Bootstrap 5**, icônes **FontAwesome**, animations **Animate.css**
- Fond d’écran avec image (`image/image11.jpg`)

##  Architecture du projet

###  Packages principaux

- `com.enit.entities`  
  - `Student`  
  - `Exam`  
  - `Session`  
  - `SessionId`  
  - `Speciality`

- `com.enit.service`  
  - Interfaces : `StudentService`, `ExamService`, `SessionService`, `SpecialityService`, `SessionIdService`  
  - Implémentations EJB stateless : `StudentServiceImpl`, `ExamServiceImpl`, etc.  
  - Utilisation de `@PersistenceContext(unitName = "UP_COURS")`

- `com.enit.controller`  
  - `StudentController`  
  - `ExamController`  
  - `SessionController`  
  - `SpecialityController`  
  - Servlets annotées avec `@WebServlet` et injectant les services via `@EJB`

###  Persistance

Fichier `persistence.xml` :

- `persistence-unit` : **UP_COURS**
- Datasource JTA : `java:/coursDS`
- Dialecte Hibernate configuré pour MySQL
- `hibernate.hbm2ddl.auto = update` (génération / mise à jour automatique du schéma)


##  Stack technique

| Composant              | Technologie                     |
|------------------------|----------------------------------|
| Langage                | Java (Jakarta EE)               |
| Web                    | JSP, Servlets, JSTL             |
| Frontend               | Bootstrap 5, FontAwesome, CSS   |
| Métier                 | EJB Stateless                   |
| Persistance            | JPA / Hibernate                 |
| Base de données        | MySQL                           |
| Configuration JPA      | `persistence.xml` (UP_COURS)    |
| Serveur d’application  | Jakarta EE (ex. WildFly, Payara)|


##  Structure simplifiée

```text
coursWeb/
 ├─ src/main/java/
 │   ├─ com/enit/entities/
 │   │   ├─ Student.java
 │   │   ├─ Exam.java
 │   │   ├─ Session.java
 │   │   ├─ SessionId.java
 │   │   └─ Speciality.java
 │   ├─ com/enit/service/
 │   │   ├─ StudentService.java / StudentServiceImpl.java
 │   │   ├─ ExamService.java / ExamServiceImpl.java
 │   │   ├─ SessionService.java / SessionServiceImpl.java
 │   │   ├─ SpecialityService.java / SpecialityServiceImpl.java
 │   │   └─ SessionIdService.java / SessionIdServiceImpl.java
 │   ├─ com/enit/controller/
 │   │   ├─ StudentController.java
 │   │   ├─ ExamController.java
 │   │   ├─ SessionController.java
 │   │   └─ SpecialityController.java
 │   └─ META-INF/
 │       └─ persistence.xml
 ├─ src/main/webapp/
 │   ├─ Home.jsp
 │   ├─ Welcome.jsp (si utilisé)
 │   ├─ image/
 │   │   └─ image11.jpg
 │   └─ WEB-INF/
 │       ├─ web.xml
 │       └─ lib/ (dépendances éventuelles)
 └─ build/


## 🎥 Démonstration Vidéo

Pour visualiser le fonctionnement complet de l’application (gestion des étudiants, examens, sessions et spécialités), une vidéo de démonstration est fournie :

**Voir la démo :**  
https://github.com/Kawthertlili/Gestion-academique-jee/blob/main/DEMO.mp4

> **Note importante :**  
> GitHub ne permet pas toujours la lecture directe des fichiers vidéo.  
> Si la vidéo ne s’ouvre pas dans le navigateur, utilisez l’option **“Download”** pour la télécharger puis la lire localement.

