# Bitácora del laboratorio de rescate

Reto 1: Ver el historial

¿Qué muestra cada comando?
- git log: Muestra todo el historial con bastante detalle: el código completo del commit, quién lo hizo, la fecha y hora, y el mensaje que se dejó.
- git log --oneline: Resume cada commit en una sola línea, mostrando solo el inicio del código y el mensaje, así es más fácil de leer rápido.
- git log --oneline --graph --all: También lo muestra resumido en una línea, pero dibuja unas líneas a la izquierda para ver cómo se dividen o se unen las ramas, e incluye todas las ramas del proyecto.

¿Qué es el código que aparece al inicio de cada commit?
Es como la cédula o identificador único de cada commit (en Git se le llama hash). Sirve para diferenciar un guardado de otro y poder referirse a él si luego toca revisar o deshacer algo.


Reto 2: Ver qué cambió antes de guardar

¿Por qué el segundo git diff no mostró nada?
Porque antes de ese segundo git diff ya había usado git add notas.txt. Eso movió los cambios al área de preparación (como listos para el commit), y git diff solo compara los cambios que todavía no se han agregado.

¿Qué muestra --staged?
Muestra justamente los cambios que ya están agregados con git add y listos para quedar en el próximo commit.


Reto 3: "Borré un archivo por error"

¿Qué hace git restore?
Descarta los cambios que no se han guardado en un commit y deja el archivo tal como estaba en el último commit (por eso pudo recuperar notas.txt después de borrarlo).

¿Funcionaría si nunca hubieras hecho commit de ese archivo?
No, porque si nunca se le hizo commit, Git no tiene ninguna copia guardada de dónde recuperarlo.


Reto 4: "Agregué un archivo que no debía subir"

¿Qué diferencia hay entre git restore y git restore --staged?
git restore deshace los cambios que hice en el archivo (lo devuelve a como estaba en el último commit, o sea que pierdo lo que modifiqué). En cambio, git restore --staged no borra mis cambios ni el archivo; solo lo saca del área de preparación (git add) para que no se incluya en el próximo commit.


Reto 5: "Escribí mal el mensaje del commit"

¿Qué hace git commit --amend?
Sirve para corregir el mensaje del último commit que hice sin tener que crear otro nuevo. Solo se debe usar cuando todavía no he hecho git push, porque si ya lo subí estaría cambiando un historial que otros compañeros pueden tener.


Reto 6: "Subí un commit que dañó el proyecto"

¿git revert borró el commit equivocado o creó uno nuevo?
No lo borró; lo que hizo fue crear un commit nuevo que revierte o deshace los cambios del commit anterior (dejando el archivo como estaba antes).

¿Por qué es la opción segura cuando ya se hizo push?
Porque no reescribe ni borra el historial que ya está en GitHub. Si mis compañeros ya habían descargado ese commit, no les va a generar conflictos ni desorden en su historial.


Reto 7: "Hice un commit antes de tiempo"

¿Qué diferencia hay entre git reset --soft y git revert?
git reset --soft borra el último commit del historial pero deja todos los archivos y cambios intactos en el área de preparación para seguir editándolos. En cambio, git revert no borra el commit viejo, sino que crea un commit nuevo que deshace lo que hizo el anterior.

¿Cuándo se usa cada uno?
git reset --soft se usa cuando el commit todavía es solo local (no he hecho git push). git revert se usa cuando ya subí el commit a GitHub y necesito deshacerlo sin dañar el historial de los demás.


Reto 8: "Tengo trabajo a medias y debo cambiar de tarea"

¿Para qué sirve git stash?
Sirve para guardar temporalmente los cambios que llevo a medias sin tener que hacer un commit incompleto, dejando la carpeta de trabajo limpia para poder cambiar de rama o hacer otra tarea urgente.

¿Qué hace git stash pop?
Saca esos cambios que había guardado en el stash, los vuelve a aplicar en mi carpeta de trabajo y los borra de la lista del stash para que yo siga trabajando donde iba.

$ git log --oneline --graph
* 4963889 (HEAD -> main, origin/main, origin/HEAD) docs: agrega línea 5 a notas
* 7089c29 (fix/urgente) feat: agrega borrador completo
* deb0d33 Revert "fix: limpia notas"
* 0d74ee8 fix: limpia notas
* 58bb71c docs: agrega línea 4 a notas
* c83fe62 chore: agrega .gitignore para archivos .env
* 13f0b01 docs: modifica línea 2 de notas
* ae341bb feat: agrego notas y bitácora
* 8fba0f7 Initial commit