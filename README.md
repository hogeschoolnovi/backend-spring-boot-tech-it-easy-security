# Opdrachtbeschrijving

## Inleiding

Je bent net begonnen als developer bij een bedrijf genaamd Tech It Easy, dat tv’s verkoopt. Tijdens de cursus Spring Boot ga jij een backend applicatie voor het bedrijf programmeren. De winkel heeft een inventaris van televisies die moet worden bijgehouden. Na iedere les gaan we deze applicatie een stukje verder uitbouwen in de vorm van huiswerk. Zo krijgen we stap-voor-stap meer ervaring in het bouwen van een backend applicatie. Aan het einde van de cursus zullen we een werkende Tech It Easy backend hebben!

## Recap van vorige opdracht

De [vorige opdracht](https://github.com/hogeschoolnovi/backend-spring-boot-tech-it-easy-relations-uitwerkingen) was een best pittige opgave, maar als alles gelukt is, heb je een applicatie met meerdere modellen en relaties gevormd. Super gaaf! Hier wordt de opdrachtgever dolblij van, maar hij vindt wel dat er veilig gebruikgemaakt moet worden van de app. Het zou niet tof zijn als de inventaris bijvoorbeeld door klanten zelf aangepast kan worden. Hiervoor moet je gaan nadenken over een inlogsysteem. Daar komt veel bij kijken. Je wilt namelijk niet dat een `Hacker` deze met gemak het inlogsysteem kan omzeilen. Daarom is het belangrijk om het inloggen te beveiligen. Dat ga je in deze opdracht doen.
 
## De opdracht
Maak de beveiliging voor de applicatie met een JWT. Zorg hierbij dat er een user(employee) aangemaakt kan worden door de admin en dat de user en admin verschillende dingen (taken) mogen/kunnen. Enkel iemand met een admin-rol mag bijvoorbeeld authorities aanmaken of verwijderen en alle users opvragen.
 
## Randvoorwaarden
De opdracht moet voldoen aan de volgende voorwaarden:
- De `POM` bevat _spring-boot-starter-parent_ versie 3.1.4
- De `POM` bevat de _spring-boot-starter-security_, _jjwt-api_, _jjwt-impl_ en _jjwt-jackson_ dependencies
- De applicatie bevat:
  - `GlobalCorsConfiguration`
  - `SpringSecurityConfig`
  - `AuthenticationController`
  - `UserController`
  - `UserDto` (of `UserDto en UserInputDto`)
  - `UsernameNotFoundException`
  - `JWTFilter`
  - `Authority`
  - `AuthorityKey`
  - `User`
  - `AuthenticationRequest`(vorm van inputDto)
  - `AuthenticationResponse` (vorm van dto)
  - `UserRepository`
  - `CustomUserDetailService`
  - `UserService`
  - `JwtUtil`
  - `RandomStringGenerator`
- Binnen de applicatie wordt rekening gehouden met CORS
- De applicatie moet draaien met toegang tot de endpoints voor de juiste gebruikers geven

### Belangrijk
- De applicatie moet geen toegang geven zonder authenticatie en identificatie;
- De applicatie heeft een user(employee)- en een admin-rol;
- De applicatie moet draaien met toegang tot de endpoints voor de juiste gebruikers;
- Los alle comments op uit de toegevoegde klassen, na het kopiëren en plakken van die klassen.

## Stappenplan

1. Voeg de volgende dependencies toe aan je POM.XML.
 - `<dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-security</artifactId>
  </dependency>`
 - ` <dependency>
   <groupId>io.jsonwebtoken</groupId>
   <artifactId>jjwt-api</artifactId>
   <version>0.11.5</version>
   </dependency>`
 - `<dependency>
   <groupId>io.jsonwebtoken</groupId>
   <artifactId>jjwt-impl</artifactId>
   <version>0.11.5</version>
   <scope>runtime</scope>
   </dependency>`
 - `<dependency>
   <groupId>io.jsonwebtoken</groupId>
   <artifactId>jjwt-jackson</artifactId>
   <version>0.11.5</version>
   <scope>runtime</scope>
   </dependency>`
 - `<!--    Deze dependency heb je nodig, omdat de versie die origineel bij Spring Boot 3.1.4 wordt geleverd een bug heeft die in dit project een error geeft voor de User-Authority relatie.    -->
        <dependency>
            <groupId>org.hibernate</groupId>
            <artifactId>hibernate-core</artifactId>
            <version>6.3.1.Final</version>
        </dependency>`
  
2. Voeg de `User`, `Authority` en de `AuthorityKey` toe als modellen.
  
3. Voeg een `UserRepository` toe aan het project.

4. Voeg de `UserDto` toe aan de applicatie.

5. Voeg een map toe genaamd `utils`. Voeg hier de `JwtUtil` en de `RandomStringGenerator` toe aan het project.
  
6. Voeg de `UserService` en de `CustomUserDetailService` toe aan het project.

7. Voeg de `BadRequestException` en de `UsernameNotFoundException` toe aan je project en zorg dat de exception handlers zijn toegevoegd in je `ExceptionController`.

8. Voeg een nieuwe map genaamd `payload`  met daarin de `AuthenticationRequest` en de `AuthenticationResponse` toe aan het project. (Je mag deze 2 ook in de `dto` map zetten.)

9. Voeg de `AuthenticationController` en de `UserController` toe aan je project.

10. Voeg de `JwtRequestFilter` toe aan je project in een map genaamd `filter`.

11. Voeg als laatste de `SpringSecurityConfig` en de `GlobalCorsConfiguration` toe aan het project.

12. Kijk goed of je in de `SpringSecurityConfig` nog requestmatchers wil/moet toevoegen.

13. Update de data.sql met users en authorities.

14. Check goed of je alle TODO-comments hebt uitgevoerd en er geen fouten meer in de applicatie zitten.

15. Injecteer in de UserService de PasswordEncoder. Zorg dat in de createUser methode het password encode wordt, zodat een nieuwe gebruiker ook kan inloggen. 

(Note: Wanneer de PasswordEncoder een "circular reference" geeft, kun je de passwordencoder bean uit de SecurityConfig halen en in een eigen configuratie klasse zetten. Zie voor de uitwerking daarvan de passwordencoder-branch van de uitwerkingen repo)

## Bonus

Zorg dat een User alleen diens eigen gebruikersgegens kan ophalen via "GET localhost:8080/user/{id}". Maak hierbij gebruik van de "SecurityContextHolder". Kijk op internet of in de JwtRequestFilter voor verdere hints over hoe je dit kunt toepassen.


