# Container image generation with Jenkins

Ha szeretnél egy docker image-t a pontos registrybe, ebbe a projektbe illesztve könnyen megoldhatod.
Ide egyszerűbb imageket tegyünk, amik buildeléséhez elegendő egyetlen Dockerfile. 
Ha olyan képet akarsz feltenni amihez kell több build step, maven, webpack, miegymás, 
lehet érdemesebb egy saját projektet nyitnod, és ezt a projektet inspirációnak használni ahhoz.

## Új image létrehozásának lépései

### Dockerfile bemásolása:
Hozz létre egy új mappát, és másold be a Dockerfileodat.

### Jenkins pipeline részek hozzáadása
