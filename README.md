Cuando un equipo de unas 3 personas trabaja en el mismo repositorio, es importante establecer un flujo de trabajo adecuado para mantener la integridad del código y facilitar la colaboración. Aquí tienes un flujo de trabajo común utilizando Git, conocido como Gitflow:

### 1. **Crear y gestionar el repositorio central**
- **Repositorio remoto (central):** Se crea un repositorio en un servicio como GitHub, GitLab o Bitbucket.
- **Clonar el repositorio:** Cada miembro del equipo clona el repositorio remoto a su máquina local.

### 2. **Establecer ramas principales**
- **`main` (o `master`):** Rama principal donde se encuentra la versión de producción del código.
- **`develop`:** Rama de desarrollo donde se integran las nuevas características antes de ser lanzadas a producción.

### 3. **Desarrollo de características**
- **Crear una rama de característica (`feature`):** Cada miembro del equipo crea una rama a partir de `develop` para trabajar en una nueva característica.
  ```sh
  git checkout -b feature/nueva-caracteristica develop
  ```
- **Trabajar en la rama:** Realizar commits en la rama de característica.
  ```sh
  git add .
  git commit -m "Descripción del cambio"
  ```

### 4. **Integración de características**
- **Finalizar la característica:** Una vez que la característica está completa, se fusiona de nuevo a `develop`.
  ```sh
  git checkout develop
  git merge --no-ff feature/nueva-caracteristica
  git branch -d feature/nueva-caracteristica
  ```
- **Subir cambios a `develop`:** Subir los cambios a la rama `develop` en el repositorio remoto.
  ```sh
  git push origin develop
  ```

### 5. **Preparar una versión**
- **Crear una rama de lanzamiento (`release`):** Cuando `develop` tiene suficientes características para una nueva versión, se crea una rama de lanzamiento.
  ```sh
  git checkout -b release/1.2.0 develop
  ```
- **Finalizar la rama de lanzamiento:** Realizar ajustes finales y fusionar a `main` y `develop`.
  ```sh
  git checkout main
  git merge --no-ff release/1.2.0
  git tag -a 1.2.0
  git checkout develop
  git merge --no-ff release/1.2.0
  git branch -d release/1.2.0
  ```

### 6. **Manejo de problemas**
- **Crear una rama de corrección (`hotfix`):** Si se encuentra un problema crítico en producción, se crea una rama de corrección a partir de `main`.
  ```sh
  git checkout -b hotfix/1.2.1 main
  ```
- **Finalizar la rama de corrección:** Una vez corregido, fusionar a `main` y `develop`.
  ```sh
  git checkout main
  git merge --no-ff hotfix/1.2.1
  git tag -a 1.2.1
  git checkout develop
  git merge --no-ff hotfix/1.2.1
  git branch -d hotfix/1.2.1
  ```

### 7. **Sincronización con el repositorio remoto**
- **Subir cambios:** Subir las ramas `main`, `develop` y cualquier otra rama relevante al repositorio remoto.
  ```sh
  git push origin main
  git push origin develop
  ```

### 8. **Revisión de código y pull requests**
- **Pull requests:** Utilizar pull requests en GitHub, GitLab o Bitbucket para revisar y discutir los cambios antes de fusionarlos.
- **Revisión y aprobación:** Otros miembros del equipo revisan y aprueban los cambios antes de fusionarlos.

Este flujo de trabajo ayuda a mantener un historial claro y organizado, facilitando la colaboración y la gestión de versiones. Cada equipo puede adaptar este flujo según sus necesidades específicas.
