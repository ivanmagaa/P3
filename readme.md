<h1>Tarefa DIG - SRI</h1>
<h2>Descripción</h2>
<p>Nesta tarefa, realizaremos diversas consultas utilizando a ferramenta <code>dig</code>, que
nos permite interactuar cos servidores DNS e obter información sobre dominios, IPs e rexistros
DNS. A continuación, explícanse paso a paso as consultas realizadas e como se identificaron as
diferentes partes das respostas.</p>
<hr />
<h2>1. Consulta "dig danielcastelao.org"</h2>
<p>Executamos a seguinte consulta para obter información sobre o dominio
<code>danielcastelao.org</code>:</p>
<p><code>
dig danielcastelao.org
</code></p>
<h3>Partes da resposta:</h3>
<ul>
<li><strong>QUERY SECTION</strong>: Aquí vese a consulta que se fixo. Neste caso, solicitamos
información sobre o dominio <code>danielcastelao.org</code>.</li>
<li><strong>ANSWER SECTION</strong>: Esta sección devolve as IPs asociadas ao dominio.
Pode incluír rexistros A (para IPv4) ou CNAME (se hai un alias).</li>
<li><strong>AUTHORITY SECTION</strong>: Aquí aparecen os servidores de nomes autoritativos,
que son os que teñen a autoridade para xestionar o dominio.</li>
<li><strong>ADDITIONAL SECTION</strong>: Información adicional sobre os servidores
autoritativos, como as súas IPs.</li>
<li><strong>IN</strong>: Indica que estamos no sistema de nomes de Internet (IN = Internet).</li>
<li><strong>A</strong>: Tipo de rexistro que devolve a dirección IPv4 asociada ao dominio.</li>
</ul>
<hr />
<h2>2. Comparación entre <code>moodle.danielcastelao.org</code> e
<code>www.danielcastelao.org</code></h2>
<p>Realizamos as consultas:</p>
<p><code>
dig moodle.danielcastelao.org
dig www.danielcastelao.org
</code></p>
<h3>Diferencias observadas:</h3>
<ul>
<li><strong>moodle.danielcastelao.org</strong>: Pode devolver un rexistro CNAME se é un alias
doutro dominio ou simplemente unha IP se é un rexistro A.</li>
<li><strong>www.danielcastelao.org</strong>: Devolve tamén rexistros A ou CNAME, dependendo
de como estea configurado.</li>
</ul>
<hr />
<h2>3. Servidores autoritativos de <code>www.danielcastelao.org</code></h2>
<p>Para atopar os servidores de DNS autoritativos, executamos:</p>
<p><code>
dig NS www.danielcastelao.org
</code></p>
<h3>Resposta:</h3>
<p>Obtemos unha lista de servidores de nomes (NS) autoritativos. É habitual que existan varios
servidores (polo menos 2) para garantir redundancia e dispoñibilidade en caso de fallo dun
deles.</p>
<hr />
<h2>4. Consultas inversas</h2>
<p>Realizamos unha consulta inversa para a IP <code>130.206.164.68</code>:</p>
<p><code>
dig -x 130.206.164.68
</code></p>
<p>Podes realizar consultas similares para outras IPs. A consulta inversa busca o nome de dominio
asociado á IP.</p>
<hr />
<h2>5. Servidor DNS consultado</h2>
<p>Para saber que servidor DNS estamos utilizando por defecto, executamos <code>dig</code>
sen parámetros:</p>
<p><code>
dig
</code></p>
<p>Na última liña vese o servidor DNS utilizado. Para cambiar o servidor DNS para unha consulta
específica, usamos a opción <code>@</code>:</p>
<p><code>
dig @8.8.8.8 www.example.com
</code></p>
<p>Neste caso, estamos utilizando o DNS de Google (8.8.8.8).</p>
<hr />
<h2>6. Rexistro SOA de <code>moodle.danielcastelao.org</code></h2>
<p>Consultamos o rexistro SOA usando o DNS de Google:</p>
<p><code>
dig @8.8.8.8 moodle.danielcastelao.org SOA
</code></p>
<p>Logo, podemos preguntar directamente ao servidor primario de
<code>danielcastelao.org</code> obtido na consulta de NS:</p>
<p><code>
dig @&lt;servidor_primario&gt; moodle.danielcastelao.org SOA
</code></p>
<hr />
<h2>7. Consulta de <code>www.elpais.com</code> e TTL</h2>
<p>Consultamos a IP de <code>www.elpais.com</code>:</p>
<p><code>
dig www.elpais.com
</code></p>
<p>Obtemos o rexistro A e o seu TTL (Time To Live). Este valor indica canto tempo queda
almacenado no cache o rexistro DNS.</p>
<hr />
<h2>8. TTL de varios dominios</h2>
<p>Realizamos consultas para observar o TTL de varios dominios:</p>
<p><code>
dig www.google.com
dig www.facebook.com
</code></p>
<p>As diferenzas no TTL poden deberse á política de cache de cada servizo, ou á frecuencia de
actualización dos rexistros DNS.</p>
<hr />
<h2>9. TTL máximo dun dominio</h2>
<p>O TTL máximo dun dominio pódese obter observando o valor máis alto do TTL nas consultas
de DNS:</p>
<p><code>
dig www.example.com
</code></p>
<hr />
<h2>10. Máquinas detrás de <code>www.google.es</code></h2>
<p>Para ver cantas máquinas (IPs) están detrás do dominio <code>www.google.es</code>,
executamos:</p>
<p><code>
dig www.google.es
</code></p>
<h3>Observación:</h3>
<p>Normalmente, devolveranse varias IPs, o que indica que Google utiliza servidores distribuídos
globalmente para balancear a carga.</p>
<hr />
<h2>11. Consulta ao servidor raíz e recursividade</h2>
<p>Para verificar se un servidor raíz (como J.ROOT-SERVERS.NET) permite consultas
recursivas:</p>
<p><code>
dig @J.ROOT-SERVERS.NET www.google.es
</code></p>
<h3>Observación:</h3>
<p>Verificamos na resposta se o servidor permite consultas recursivas. Normalmente, os
servidores raíz non fan resolución recursiva.</p>
<hr />
<h2>12. Ver todas as queries dun DNS</h2>
<p>Para ver todas as queries dun DNS, usamos a opción <code>+trace</code>:</p>
<p><code>
dig +trace www.timesonline.co.uk
</code></p>
<hr />
<h2>13. Servidores de correo de <code>danielcastelao.org</code></h2>
<p>Para saber os servidores de correo (MX) dun dominio:</p>
<p><code>
dig danielcastelao.org MX
</code></p>
<p>Devolve os servidores de correo e as súas prioridades.</p>
<hr />
<h2>14. Rexistros AAAA de <code>www.facebook.com</code></h2>
<p>Podemos consultar os rexistros AAAA, que son os rexistros de IPv6:</p>
<p><code>
dig www.facebook.com AAAA
</code></p>
<p>Se existen rexistros AAAA, devolven as direccións IPv6 de Facebook.</p>
