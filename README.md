



``` 
 ▄▄▄       █    ██ ▄▄▄█████▓ ▒█████   ██▓███   █    ██   ██████  ██░ ██       ██▓███ ▓██   ██▓
▒████▄     ██  ▓██▒▓  ██▒ ▓▒▒██▒  ██▒▓██░  ██▒ ██  ▓██▒▒██    ▒ ▓██░ ██▒     ▓██░  ██▒▒██  ██▒
▒██  ▀█▄  ▓██  ▒██░▒ ▓██░ ▒░▒██░  ██▒▓██░ ██▓▒▓██  ▒██░░ ▓██▄   ▒██▀▀██░     ▓██░ ██▓▒ ▒██ ██░
░██▄▄▄▄██ ▓▓█  ░██░░ ▓██▓ ░ ▒██   ██░▒██▄█▓▒ ▒▓▓█  ░██░  ▒   ██▒░▓█ ░██      ▒██▄█▓▒ ▒ ░ ▐██▓░
 ▓█   ▓██▒▒▒█████▓   ▒██▒ ░ ░ ████▓▒░▒██▒ ░  ░▒▒█████▓ ▒██████▒▒░▓█▒░██▓ ██▓ ▒██▒ ░  ░ ░ ██▒▓░
 ▒▒   ▓▒█░░▒▓▒ ▒ ▒   ▒ ░░   ░ ▒░▒░▒░ ▒▓▒░ ░  ░░▒▓▒ ▒ ▒ ▒ ▒▓▒ ▒ ░ ▒ ░░▒░▒ ▒▓▒ ▒▓▒░ ░  ░  ██▒▒▒ 
  ▒   ▒▒ ░░░▒░ ░ ░     ░      ░ ▒ ▒░ ░▒ ░     ░░▒░ ░ ░ ░ ░▒  ░ ░ ▒ ░▒░ ░ ░▒  ░▒ ░     ▓██ ░▒░ 
  ░   ▒    ░░░ ░ ░   ░      ░ ░ ░ ▒  ░░        ░░░ ░ ░ ░  ░  ░   ░  ░░ ░ ░   ░░       ▒ ▒ ░░  
      ░  ░   ░                  ░ ░              ░           ░   ░  ░  ░  ░           ░ ░     
                                                                          ░           ░ ░     
````


> Guía de configuración y automatización
## 1. Requisitos

Antes de usar el programa asegúrate de tener:

- Git instalado en el sistema (`git --version` para verificar)
- Una carpeta con repositorio Git inicializado (`git init`)
- Acceso configurado a GitHub/GitLab (SSH o HTTPS con token)

---

## 2. Configuración inicial

### Editar config.txt

Abre el archivo `config.txt` que está en la misma carpeta que el ejecutable y escribe la ruta a tu carpeta:

```
C:/Users/TuUsuario/Documents/MiCarpeta
```

Guarda y cierra el archivo. Solo necesitas hacer esto una vez.

### Archivos incluidos

- `backup.exe` — El ejecutable principal
- `config.txt` — Aquí escribes la ruta de tu carpeta
- `log.txt` — Se crea automáticamente, registra cada backup realizado

---

## 3. Automatizar con el Programador de Tareas de Windows

### Paso 1 — Abrir el Programador de Tareas

1. Presiona las teclas `Windows + R`
2. Escribe `taskschd.msc` y presiona Enter
3. Se abre el Programador de tareas de Windows

### Paso 2 — Crear una tarea nueva

1. En el panel derecho haz clic en **Crear tarea básica**
2. Asigna un nombre, por ejemplo: `Obsidian Backup`
3. Haz clic en **Siguiente**

### Paso 3 — Configurar el desencadenador (cuándo se ejecuta)

1. Selecciona la frecuencia que prefieras: Diariamente, Semanalmente, etc.
2. Configura la hora a la que quieres que corra el backup
3. Haz clic en **Siguiente**

### Paso 4 — Configurar la acción (qué ejecutar)

1. Selecciona **Iniciar un programa**
2. Haz clic en **Siguiente**
3. En el campo **Programa o script** haz clic en Examinar y selecciona `backup.exe`
4. En **Iniciar en** escribe la ruta de la carpeta donde está el `backup.exe` 

```
C:\Users\TuUsuario\Desktop\backup\backup.exe
```

> ⚠️ **Este campo es importante:** si no lo llenas, el programa no encontrará el `config.txt`.

### Paso 5 — Finalizar

1. Haz clic en **Siguiente** y luego en **Finalizar**
2. La tarea aparecerá en la lista del Programador de tareas
3. Para probarla, haz clic derecho sobre la tarea y selecciona **Ejecutar**

---

## 4. Verificar que el backup funcionó

Después de cada ejecución puedes verificar en dos lugares:

- Revisa el archivo `log.txt` — debe tener una nueva línea con la fecha y hora del backup
- Entra a tu repositorio en GitHub/GitLab y verifica que aparezca un nuevo commit con el mensaje `Backup` seguido de la fecha

---

## 5. Solución de problemas comunes

**El programa no encuentra config.txt**

- Asegúrate de que `config.txt` está en la misma carpeta que `backup.exe`
- Verifica que llenaste el campo **Iniciar en** en el Programador de tareas

**Error de autenticación al hacer push**

- Verifica que tienes acceso configurado a GitHub (SSH key o token HTTPS)
- Prueba ejecutando `git push` manualmente en la carpeta para confirmar que funciona

**No se genera ningún commit**

- Si no hay cambios en la carpeta, GitPython no crea un commit vacío
- Esto es normal, el `log.txt` igual registrará la ejecución si no hubo errores

El script fue creado con el propósito de automatizar una copia de respaldo de notas de obsidian subiéndolas a un repositorio en GitHub con git, pero realmente funciona con cualquier repositorio.