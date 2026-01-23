Tehnoloogiad
Backend: Java 17, Spring Boot 2.7.16, Spring Data JPA, Hibernate, Maven.
Frontend: React, Node.js (hallatakse Maveni kaudu).
Andmebaas: H2 (mälupõhine arenduseks), PostgreSQL tugi olemas.
Konteinerid: Jib (Docker/OCI image loomiseks).
Testandmed: JavaFaker.

Eeltingimused
Enne alustamist veendu, et sul on installitud:
Java 17
Maven 3.x
(Valikuline) Node.js & npm (kui soovid frontendi eraldi arendada).

Rakenduse käivitamine
1. Rakenduse ehitamine (Build)
Kogu projekti (nii backendi kui ka frontendi) ehitamiseks kasuta Mavenit:
code
mvn clean install

2. Rakenduse käivitamine
Pärast edukat ehitamist saad rakenduse käivitada käsuga:
code
java -jar target/full-stack-spring-boot-react-0.0.1-SNAPSHOT.jar
Rakendus on kättesaadav aadressil: http://localhost:8080
Andmebaas
Rakendus kasutab arendusrežiimis mälupõhist H2 andmebaasi.
H2 Console: http://localhost:8080/h2-console
JDBC URL: jdbc:h2:mem:medinardb
Username: sa
Password: (tühi)

Arendusrežiim
Frontendi arendus
Kui soovid Reacti koodi muuta ja näha muudatusi reaalajas (Hot Reload), mine frontendi kataloogi ja käivita see eraldi:
code
Bash
cd src/frontend
npm install
npm start
Märkus: Sel juhul peab backend (Spring Boot) samuti taustal töötama.
Backendi arendus
Käivita Spring Booti 
Docker ja Jib
Projekt kasutab Jib pluginat Docker image'ite loomiseks ilma Dockerfile'ita.
Image'i loomine kohalikku Dockerisse:
code
Bash
mvn compile jib:dockerBuild -Pjib-push-to-local -Dapp.image.tag=v1
Image'i saatmine Docker Hubi:
code
Bash
mvn compile jib:build -Pjib-push-to-dockerhub -Dapp.image.tag=v1
ailid (genereeritakse pärast npm run build).
pom.xml - Maveni seadistused ja frontend-maven-plugin konfiguratsioon.
