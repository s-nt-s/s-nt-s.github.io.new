Title: Algunos datos sobre Menéame 2: Strikes
Category: Datos
body_class: overgraph
tags: Menéame
SOURCE: https://s-nt-s.github.io/meneame.dump/i2/index.html


<div><script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script><script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/2.9.3/Chart.min.js"></script><script data-autoinsert="1" src="https://s-nt-s.github.io/meneame.dump/00-libs/sigma.min.js"></script><script data-autoinsert="1" src="https://s-nt-s.github.io/meneame.dump/00-libs/sigma.plugins.animate.min.js"></script><script data-autoinsert="1" src="https://s-nt-s.github.io/meneame.dump/00-libs/tagify.js"></script><script data-autoinsert="1" src="https://s-nt-s.github.io/meneame.dump/01-js/00-util.js"></script><script data-autoinsert="1" src="https://s-nt-s.github.io/meneame.dump/01-js/01-tag.js"></script><script data-autoinsert="1" src="https://s-nt-s.github.io/meneame.dump/01-js/02-chart.js"></script><script data-autoinsert="1" src="https://s-nt-s.github.io/meneame.dump/i2/data/00-modelos.js"></script><script data-autoinsert="1" src="https://s-nt-s.github.io/meneame.dump/i2/data/modelos.js"></script><script data-autoinsert="1" src="https://s-nt-s.github.io/meneame.dump/i2/js/00-graph.js"></script><script data-autoinsert="1" src="https://s-nt-s.github.io/meneame.dump/i2/js/00-tag.js"></script><script data-autoinsert="1" src="https://s-nt-s.github.io/meneame.dump/i2/js/chart.js"></script><link href="https://yaireo.github.io/tagify/dist/tagify.css" rel="stylesheet" type="text/css"/><link data-autoinsert="1" href="https://s-nt-s.github.io/meneame.dump/css/main.css" rel="stylesheet" type="text/css"/>
<p>
      En el <a href="https://s-nt-s.github.io/meneame_en_datos/">anterior informe sobre Menéame</a>
      expliqué brevemente por qué no iba a analizar los strikes.
      Sin embargo, finalmente me he animado a ello y aquí tenéis los resultados.
    </p><p>
</p><h2>Consideraciones previas</h2>
<p>
      Antes de empezar vamos a tratar unos puntos claves para contextualizar los datos:
    </p>
<ol>
<li>
        La funcionalidad de strikes se implementó en algún momento
        posterior al <a href="https://github.com/Meneame/meneame.net/blob/master/sql/2017-02-24-strikes.sql">24/02/2017</a>
        pero no he encontrado ningún comunicado oficial y fechado de cuando
        entró en vigor, así que usaremos como referencia la fecha del
        primer strike detectado (<code>07/04/2017</code>).
      </li>
<li>
        En <a href="https://www.meneame.net/normas-comunidad">las normas de Menéame</a>
        se pueden consultar el significado de la mayor parte de tipos de strikes.
      </li>
<li>
        En <a href="https://www.meneame.net/legal#penalizaciones">la información legal de Menéame (apartado Penalizaciones)</a>
        podemos consultar las consecuencias de los strikes (ninguna conlleva la eliminación de la cuenta o el ban perpetuo).
      </li>
<li>
<a href="https://blog.meneame.net/2019/03/26/revision-de-las-normas-de-uso-de-la-comunidad-hacia-una-conversacion-mas-sana/" title="2019-03-26 Revisión de las normas de uso de la comunidad: hacia una conversación más sana">En 26/03/2019 la administración de Méneame</a>:
        <ul>
<li>indica que se reciben muchas quejas por los strikes</li>
<li>
            recuerda que la administración no da strikes proactivamente,
            si no que solo se revisan comentarios previamente reportados por los usuarios
            (en la <a href="https://github.com/Meneame/meneame.net/wiki/Abusos">wiki</a>
            también se dice que la mayoría de los reportes se desestiman)
          </li>
<li>aclara que aunque un strike queda asociado a un único
            comentario este puede estar motivado por la reiteración de
            comentarios o comportamientos</li>
<li>anuncia que para mejorar la transparencia próximamente habrá un método
          para que todos los usuarios pudan saber si un comentario ha sido objeto
          de strike</li>
</ul>
</li>
<li>
        En cuanto el último punto (el de la transparencia) no sé si se ha llegado a implementar.
        La realidad es que lo único que denota que un comentario tiene un strike
        es una <a href="https://github.com/Meneame/meneame.net/blob/60fc5935e46fb72c47945abc63cd062803d030a8/www/libs/comment.php#L370">clase incluida en el html</a> lo cual se traduce en un comentario plegado
        y en gris. Inspeccionando el código se puede <a href="https://github.com/Meneame/meneame.net/blob/60fc5935e46fb72c47945abc63cd062803d030a8/www/templates/comment_summary_text.html#L3">recuperar la razón del strike</a> y el <code>id</code>
        del comentario, con el cual podemos posteriormente recuperar el contenido del comentario.
        Así que aunque es posible, con un poco de maña, identificar
        los comentarios con strike, no creo a que ésta sea la mejora
        a la que se refería la administración en su blog.
      </li>
<li>
        La Api de Menéame no devuelve ninguna información sobre strikes.
      </li>
</ol>
<p>Sabiendo todo esto, podemos continuar teniendo en cuenta
      que todos los datos aquí presentados parten de recolectar
      única y exclusivamente los strikes detectados
      en comentarios inspeccionando código HTML, es decir,
      si hay (que parece que no, pero no lo sé a ciencia cierta)
      algún tipo de strike que no se asocia a comentarios
      de la manera que hemos visto quedará fuera del estudio.
    </p>
<h2>¿Cuántos strikes hay?</h2>
<p>
      Se han capturado <code>486 strikes</code>
      desde <code>07/04/2017</code> hasta
      <code>31/12/2020</code>
      repartidos de la siguiente manera:
    </p>
<table>
<thead style="text-align: center;">
<tr>
<th colspan="2">Strike</th>
<th rowspan="2">Usuarios<sup>1</sup></th>
<th colspan="2">Visto</th>
</tr><tr>
<th>#</th>
<th>Razón</th>
<th>desde<sup>2</sup></th>
<th>hasta<sup>3</sup></th>
</tr>
</thead>
<tbody>
<tr>
<td class="rg"><code>197</code></td>
<td>Insultos directos</td>
<td class="rg"><code>177</code></td>
<td><code>07/04/2017</code></td>
<td><code>28/12/2020</code></td>
</tr>
<tr>
<td class="rg"><code>131</code></td>
<td>Incitación al odio</td>
<td class="rg"><code>113</code></td>
<td><code>12/06/2017</code></td>
<td><code>30/12/2020</code></td>
</tr>
<tr>
<td class="rg"><code>127</code></td>
<td>Contenido inapropiado</td>
<td class="rg"><code>115</code></td>
<td><code>15/04/2017</code></td>
<td><code>23/12/2020</code></td>
</tr>
<tr>
<td class="rg"><code>9</code></td>
<td>Bulo</td>
<td class="rg"><code>9</code></td>
<td><code>02/05/2020</code></td>
<td><code>28/12/2020</code></td>
</tr>
<tr>
<td class="rg"><code>8</code></td>
<td>Viola las normas de uso</td>
<td class="rg"><code>8</code></td>
<td><code>17/08/2017</code></td>
<td><code>09/04/2020</code></td>
</tr>
<tr>
<td class="rg"><code>5</code></td>
<td>Spam</td>
<td class="rg"><code>5</code></td>
<td><code>17/09/2018</code></td>
<td><code>09/12/2020</code></td>
</tr>
<tr>
<td class="rg"><code>3</code></td>
<td>Incumple la legalidad española vigente</td>
<td class="rg"><code>3</code></td>
<td><code>21/07/2017</code></td>
<td><code>26/10/2018</code></td>
</tr>
<tr>
<td class="rg"><code>2</code></td>
<td>Contiene datos personales propios o de un tercero</td>
<td class="rg"><code>2</code></td>
<td><code>19/08/2017</code></td>
<td><code>03/10/2017</code></td>
</tr>
<tr>
<td class="rg"><code>2</code></td>
<td>Material pornográfico o de violencia gráfica</td>
<td class="rg"><code>2</code></td>
<td><code>06/10/2019</code></td>
<td><code>25/11/2019</code></td>
</tr>
<tr>
<td class="rg"><code>2</code></td>
<td>Promoción comercial de productos o servicios</td>
<td class="rg"><code>2</code></td>
<td><code>01/08/2017</code></td>
<td><code>01/08/2017</code></td>
</tr>
</tbody>
</table>
<p>Notas:</p>
<ol>
<li>Usuarios únicos, es decir: ¿Cuántos usuarios <b>distintos</b> tienen uno o más strikes de este tipo?</li>
<li>Primera fecha en la que se vió un strike de este tipo</li>
<li>Última fecha en la que se vió un strike de este tipo</li>
</ol>
<p>
      En números absolutos, ha habido aproximadamente
      un strike cada <code>3</code> días
      y se han visto afectados un total de
      <code>398</code> usuarios.
    </p>
<p>
      En otras palabras, entre <code>07/04/2017</code> y
      <code>31/12/2020</code>
      el <code title="486 de 10.294.798">0.005%</code> de los comentarios
      recibieron un strike y el
      <code title="398 de 33.575">1%</code> de los usuarios
      que hicieron esos comentarios recibieron un strike o más.
    </p>
<p>
<b>¿Qué vemos aquí?</b>
</p>
<p>
      Lo primero que llama la atención es que esta lista de strikes
      no coincide con las <a href="https://github.com/Meneame/meneame.net/blob/60fc5935e46fb72c47945abc63cd062803d030a8/www/templates/report_new.html#L10">opciones que ve el usuario cuando reporta un comentario</a>.
      Consultando la clase <a href="https://github.com/Meneame/meneame.net/blob/master/www/libs/strike.php#L11">strike en el código fuente</a> comprobamos que nuestra lista es correcta
      (solo falta <code>Bulo</code> y seguramente sea porque el repositorio no está actualizado),
      y si consultamos el <a href="https://github.com/Meneame/meneame.net/commits/master/www/templates/report_new.html">histórico del formulario</a> verificamos que algunas opciones no estaban disponibles en el momento que se usaron.<br/>
      Solo se me ocurren dos explicaciones:
    </p>
<ol>
<li>Los admin pueden dar strikes usando una lista más amplia que el resto de los usuarios</li>
<li>No hay una correspondencia 1 a 1 entre <code>reporte</code> y strike
    	si no que existe un un paso intermedio entre que se da por bueno un <code>reporte</code>
    	y se asigna el strike definitivo, pudiendo éste ser cambiado por otro que el admin
    	juzgue más descriptivo, por ejemplo rebajando un reporte por <code>incitación al odio</code> a
    	<code>contenido inapropiado</code></li>
</ol>
<p>La primera opción entra en conflicto con lo dicho más arriba sobre que solo se
    revisan comentarios reportados por los usuarios así que voy a suponer que la correcta
    es la segunda opción.</p>
<p>
    	Sea como sea, esto dificulta interpretar los datos como un subconjunto
    	fiel de lo que reportan los usuarios ya que, por ejemplo, ¿qué reportaron los usuarios
    	que alertaron sobre los comentarios que finalmente quedaron marcados con un
    	strike <code>contenido inapropiado</code>? No se puede saber.
    </p>
<p>Aún así vemos una división tan clara entre las tres primeras causas de strike
    y el resto que podríamos pensar que las normas con menos strikes son:</p>
<ul>
<li>normas que apenas se incumplen</li>
<li>normas que se incumplen pero a los usuarios no les importa demasiado</li>
<li>normas que se incumplen pero los usuarios piensan que no son
            merecedoras de un strike y lo dejan en un voto negativo
            a lo sumo</li>
</ul>
<p>La única excepción podría ser el <code>strike Bulo</code> ya que viendo
        su primera fecha de uso parece que es de muy reciente creación
        y aún así ya esta en la 4ª posición.</p>
<p>Lo segundo que llama la atención son las cantidades en sí.
        <a href="https://blog.meneame.net/2019/03/26/revision-de-las-normas-de-uso-de-la-comunidad-hacia-una-conversacion-mas-sana/">La
        afirmación por parte de la administración de que recibe muchas
        quejas</a> por los strikes y los abundantes
        <a href="https://www.meneame.net/m/Art%C3%ADculos/search?q=strike">artículos</a>
        y <a href="https://www.meneame.net/search?q=strike&amp;w=comments&amp;h=&amp;o=&amp;u=">comentarios</a>
        quejándose de los strikes me hacían pensar que habría muchos más strikes y usuarios afectados.
        Puede que el problema sean mis expectativas iniciales, o que yo nunca
        haya administrado un foro, pero ahora no puedo evitar pensar
        que la cantidad de strikes es minúscula.
      </p>
<p>
      A partir de aquí, viendo la poca relevancia que tienen los strikes
      me temo que el interés (y el morbo) por este estudio pierde muchos enteros.
      Sin embargo, ya que tengo los datos... continuemos.
    </p>
<h2>¿Cuál ha sido la evolución temporal de los strikes?</h2>
<div class="data" data-modelo="timeline">
<p>Mostrar cantidad de strikes en <select name="transformacion">
<option selected="selected" value="">números absolutos</option>
<option value="porcentaje">% del total</option>
<option value="comentarios">promedio por comentario</option>
<option value="usuarios">promedio por usuario</option>
</select>
</p>
<canvas class="chart"></canvas>
<p>
<label>Unidad temporal:</label>
<select name="agrupar">
<option value="">mes</option>
<option selected="selected" value="trimestre">trimestre</option>
<!--option value="cuatrimestre">cuatrimestre</option-->
<option value="semestre">semestre</option>
<option value="year">anual</option>
</select>
</p>
</div>
<p>
<b>¿Qué vemos aquí?</b>
</p>
<p>
      Poca cosa, la verdad. La grafica es muy irregular, no hay una
      tendencia clara ni a peor ni a mejor.
      Personalmente, leyendo las quejas, me esperaba que la gráfica
      fuera una linea claramente ascendente al menos en los dos
      tipos de strikes más polemicos (insultos y odio)
      pero ni eso, incluso bajan más que subir.
    </p>
<h2>¿Hay usuarios con muchos strikes?</h2>
<p>Los <code>398</code> usuarios con strikes
      se dividen en:
    </p>
<ul>
<li>
<code>1</code> usuario que ha recibido <code>5 strikes</code>
</li>
<li>
<code>4</code> usuarios que han recibido <code>4 strikes</code> cada uno
                      </li>
<li>
<code>19</code> usuarios que han recibido <code>3 strikes</code> cada uno
                      </li>
<li>
<code>34</code> usuarios que han recibido <code>2 strikes</code> cada uno
                      </li>
<li>
<code>340</code> usuarios que han recibido <code>1 strikes</code> cada uno
                      </li>
</ul>
<p>
      Lo que según <a href="https://www.meneame.net/legal#penalizaciones">las penalizaciones</a>
      hace un computo global de <code>40</code> días de ban y <code>-20</code> puntos de karma.
    </p>
<p><b>¿Qué vemos aquí?</b></p>
<p>
      Parece que muy pocos usuarios tienen problemas recurrentes con los strikes,
      lo que puede deberse a que:
    </p>
<ol>
<li>realmente los usuarios cambian su comportamiento</li>
<li>los usuarios no cambian pero la administración se resiste a escalar el conflicto</li>
<li>los usuarios con strike terminan abandonando la plataforma</li>
<li>los usuarios con strike no cambian de comportamiento pero sí de usuario, registrando una nueva cuenta</li>
</ol>
<p>Las dos primeras hipótesis no se pueden verificar, pero las otras dos
      serán estudiadas más adelante</p>
<h2>¿Provocan los strikes el abandono de los usuarios penalizados?</h2>
<p>
      Es imposible validar completamente esta hipótesis porque incluso habiendo abandono
      este puede ser por otra causa, pero si esto fuera cierto (que se abandonó la plataforma por el strike)
      deberíamos ver en cada usuario una correlación
      entre la fecha de su último strike y el momento en que dejó Menéame.
    </p>
<div class="data" data-modelo="abandono">
<p>
        Generar gráfica con usuarios que estuvieran en Menéame
         <select name="presencia">
<option value="">más de 0 días (todos)</option>
<option value="1">más de 1 día</option>
<option value="15">más de 15 días</option>
<option value="30">más de 1 mes</option>
<option selected="selected" value="180">más de 6 meses</option>
<option value="365">más de 1 año</option>
</select><sup>1</sup>
        y tomando como referencia la <select name="abandono">
<option value="abandono">fecha de abandono o eliminación</option>
<option value="eliminacion">fecha de eliminación</option>
</select><sup>2</sup>
</p>
<canvas class="chart"></canvas>
<ol>
<li>
    	Un usuario que en poco tiempo se crea una cuenta, recibe un strike y abandona la cuenta
    	parece más el perfil de un bot, troll o spammer. Sin embargo, nuestro objetivo es detectar
    	usuarios auténticos que tras recibir un strike se marchan desilusionados.
      Usa este selector para definir la permanencia mínima
    	que consideres necesaria.
    	</li>
<li>
    	No voy a repetir aquí cómo se calcula la fecha de abandono y eliminación
    	(ya se explicó en el <a href="https://s-nt-s.github.io/meneame_en_datos/">punto
      2.B del anterior informe</a>) pero basta decir que al ser distintas
      deberías seleccionar la opción que te parezca más acertada.
    	</li>
<li>
    	Si tienes dificultades en comparar las barras más pequeñas
    	puedes <label for="nostay">
          ocultar la barra de usuarios que permanecen
          haciendo click aquí <input id="nostay" name="nostay" type="checkbox"/>
        para reescalar las demás</label>.
    	</li>
</ol>
<p><b>¿Qué vemos aquí?</b></p>
<p>
    Aunque hay una parte reseñable de usuarios que abandonan el mismo día
    que reciben el strike o en menos de un mes la inmensa mayoría
    permanecen en Menéame o tardan tanto tiempo en dejarlo que es difícil
    ver la relación entre un hecho y el otro.
    </p>
<p>
    En definitiva, aunque hay usuarios que abandonan tras el strike eso no
    explica que la mayoría de los usuarios con strikes solo tengan uno.
    </p>
</div>
<h2>¿De qué época son los usuarios con strikes?</h2>
<p>
      Si los usuarios con strikes crean nuevas cuentas con las que finalmente
      reciben otro strike llegará
      un momento en que las cuentas de 2017 (año en que se implementaron
      los strikes) o posteriores tendrán más strikes de las que les correspondería
      en una distribución usual porque la mayoría de los usuarios conflictivos
      - al haberse hecho cuentas nuevas - tendrán como fecha de registro 2017 o posterior.
      Por eso la pregunta
      <em>¿los usuarios con strike crean nuevas cuentas y vuelven a tener
        otro strike?</em> se transforma en <em>¿de qué época son los usuarios
          con strikes?</em>.
    </p>
<p>
    En esta gráfica podemos ver superpuesto la composición de
    los usuarios con strikes (rojo) y la composición de usuarios que mandaron comentarios
    a Meneáme entre <code>07/04/2017</code> y
    <code>31/12/2020</code> (azul).
    </p>
<div class="data" data-modelo="poblacion">
<canvas class="chart"></canvas>
</div>
<p><b>¿Qué vemos aquí?</b></p>
<ul>
<li>Se verifica que la distribiución es más o menos la esperada hasta 2017</li>
<li>
      Vemos que los peores años fueron de 2017 a 2019 pero que la tendencia
      se invierte en 2020 a pesar del meme <a href="https://www.meneame.net/search?q=en+meneame+desde+2020&amp;w=comments&amp;h=&amp;o=&amp;u=">
<em>en Menéame desde 2020</em></a> que hace referencia
        a la teoría de que recientemente - y con relación a la crisis COVID-19 -
        se están creando usuarios <em>fake</em>
        para trolear (cierto o no, se ve que no tiene un reflejo en strikes).
    </li>
</ul>
<p>
      Obviamente, esta grafica no es una demostración al 100% de la hipótesis
      (puede haber otras explicaciones al efecto 2017-2019 que no esté teniendo en cuenta)
      pero por lo menos no se ve desmentida por los datos (como sí pasaba con la
      anterior hipótesis).
    </p>
<p>
      Por otro lado, si damos por buena esta hipotesis, además de lo dicho
      debemos concluir que las personas afectadas por los strikes
      no son <code>398</code> si no muchas menos
      ya que es gente que opera varias cuentas.
    </p>
<h2>¿Alguna conclusión?</h2>
<p>
      No.
    </p>
</div>