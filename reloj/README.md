# Control de horario (tablet)

Página única para marcar entrada y salida y llevar la cuenta de las horas de más y
de menos, con la plata que eso significa sobre el sueldo mensual.

**La base de datos está en la propia página**: todo se guarda en el navegador de la
tablet (`localStorage`). No hay servidor, no hay cuenta que crear, no se manda nada
a ninguna parte. Funciona sin internet.

Se abre acá: <https://5egaloz.github.io/revision-google/reloj/>

Primero: ⚙ → poner el sueldo, el horario y los días de trabajo, y ponerle una clave
a los ajustes. Después, *Ver el mes y las horas* muestra el saldo.

⚠️ Los datos viven en esa tablet y en ese navegador. Bajar el respaldo (⚙ → *Bajar
respaldo*) de vez en cuando: si se borran los datos del navegador, se pierden.

Documentación larga: `sitios-vm/asistencia/LEEME.md` en el repo `memoria-vault`.
