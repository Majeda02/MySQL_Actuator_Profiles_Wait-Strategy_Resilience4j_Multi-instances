# Microservice observable & résilient avec MySQL + Actuator + Profiles + Wait Strategy + Resilience4j + Multi-instances

## Vue d’ensemble
On va construire 2 microservices :
* pricing-service
Un petit service qui renvoie un prix. Il peut “tomber en panne” * volontairement pour tester la robustesse.
book-service
Un service qui gère des livres (titre, auteur, stock) dans une base MySQL.
Quand on emprunte un livre, book-service :
    * décrémente le stock en base
    * appelle pricing-service pour récupérer un prix
    * si pricing-service est en panne, book-service ne doit pas planter ⇒ il doit continuer avec un fallback.
Ensuite on déploie tout dans Docker Compose :
* une base MySQL (avec volume pour garder les données)
* pricing-service
* 3 instances de book-service (comme en production)
* et on met une wait strategy pour éviter que book-service démarre avant MySQL (erreur classique).

## Ce que le lab produit à la fin
* pricing-service (port machine 8082) : renvoie un prix, peut simuler une panne
* book-service en 3 instances :
   * instance 1 : port machine 8082
   * instance 2 : port machine 8083
   * instance 3 : port machine 8085
* mysql (port machine 3306) + volume pour garder les données

## Objectif
* Actuator : “comment vérifier si un service est vivant et prêt”
* Healthcheck Docker : “comment Docker sait qu’un service est OK”
* Profiles Spring : “comment changer la config selon l’environnement”
* MySQL volume : “comment garder les données après redémarrage”
* Wait strategy : “comment attendre MySQL avant démarrer l’app”
* Résilience : retry + circuit breaker + fallback (Resilience4j)
* Multi-instances : pourquoi synchronized ne marche plus et comment faire avec un verrou DB

## Prérequis
* JDK 17 ou 21
* Maven 3.9+
* Docker + Docker Compose (v2 conseillé)
  
## Convention de packages
* pricing-service : com.example.pricingservice
* book-service : com.example.bookservice
  
## Arborescence finale


## Création du projet 
<img width="960" height="470" alt="Capture d&#39;écran 2026-01-11 154938" src="https://github.com/user-attachments/assets/490e6fb7-1eef-4380-af86-4a57875b7bea" />
<img width="960" height="474" alt="Capture d&#39;écran 2026-01-11 155140" src="https://github.com/user-attachments/assets/3ad1d8f3-733e-4310-b7c4-5fd257fcbbad" />

## Exécution 
<img width="960" height="504" alt="Capture d&#39;écran 2026-01-11 161843" src="https://github.com/user-attachments/assets/8d88d850-e88d-46b2-853b-8afc7e5c30c2" />
<img width="960" height="473" alt="Capture d&#39;écran 2026-01-11 161921" src="https://github.com/user-attachments/assets/a2b405c7-644a-4c5d-964f-fa185c8b888a" />
<img width="960" height="471" alt="Capture d&#39;écran 2026-01-11 161943" src="https://github.com/user-attachments/assets/1a948569-3458-4193-b7f9-bfc6d4036990" />
<img width="960" height="463" alt="Capture d&#39;écran 2026-01-11 162005" src="https://github.com/user-attachments/assets/99c35fd6-9ea7-4a25-ba82-42ecdd0b04b5" />
<img width="959" height="469" alt="Capture d&#39;écran 2026-01-11 162041" src="https://github.com/user-attachments/assets/91dcf524-9a45-4f13-b7f6-956a50e1428b" />
<img width="960" height="504" alt="Capture d&#39;écran 2026-01-11 164925" src="https://github.com/user-attachments/assets/599bba6d-bee7-4ded-92a2-969e247854f5" />
<img width="960" height="466" alt="Capture d&#39;écran 2026-01-11 165700" src="https://github.com/user-attachments/assets/f3255e39-c828-4473-855b-05cc46c9f702" />
<img width="960" height="491" alt="image" src="https://github.com/user-attachments/assets/4f8402d1-28b9-415b-9cf7-b2af050fe69e" />

## Auteur
* Nom : BEN-LAGHFIRI Majeda
* Cours: Architecture Microservices : Conception, Déploiement et Orchestration
* Date : Janvier 2026
* Encadré par : Pr.Mohamed LACHGAR







