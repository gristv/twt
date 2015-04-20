# twt

***Tecnologias implicadas***: Maven, Quartz Cluster  y Job Persistence, Spring, Mybatis.<br>
***BBDD***. Tanto las tablas propias de la app como las que requiere Quartz Cluster se implementan sobre Postgresql.<br>
***Servidores***. Apache (XAMPP) para servir los archivos xml que simulan los mensajes a publicar y Tomcat contenedor Java.<br>

```sql
--
-- TOC entry 170 (class 1259 OID 509326)
-- Name: cuenta_twitter; Type: TABLE; Schema: public; Owner: renfe; Tablespace: 
--

CREATE TABLE cuenta_twitter (
    id_negocio numeric(10,0) NOT NULL,
    cuenta text,
    idioma_por_defecto text NOT NULL,
    consumer_key text,
    consumer_secret text,
    token text,
    token_secret text,
    hashtag_lineas text
);

[...]

```
