# twt

***Tecnologias implicadas***: Maven, Quartz Cluster  y Job Persistence, Spring, Mybatis.<br>
***BBDD***. Tanto las tablas propias de la app como las que requiere Quartz Cluster se implementan sobre Postgresql.<br>
***Servidores***. Apache (XAMPP) para servir los archivos xml que simulan los mensajes a publicar y Tomcat contenedor Java.<br>

```
#!sql
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


ALTER TABLE public.cuenta_twitter OWNER TO renfe;

--
-- TOC entry 177 (class 1259 OID 517707)
-- Name: qrtz_blob_triggers; Type: TABLE; Schema: public; Owner: renfe; Tablespace: 
--

CREATE TABLE qrtz_blob_triggers (
    trigger_name character varying(200) NOT NULL,
    trigger_group character varying(200) NOT NULL,
    blob_data bytea
);


ALTER TABLE public.qrtz_blob_triggers OWNER TO renfe;

--
-- TOC entry 179 (class 1259 OID 517733)
-- Name: qrtz_calendars; Type: TABLE; Schema: public; Owner: renfe; Tablespace: 
--

CREATE TABLE qrtz_calendars (
    calendar_name character varying(200) NOT NULL,
    calendar bytea NOT NULL
);


ALTER TABLE public.qrtz_calendars OWNER TO renfe;

--
-- TOC entry 176 (class 1259 OID 517694)
-- Name: qrtz_cron_triggers; Type: TABLE; Schema: public; Owner: renfe; Tablespace: 
--

CREATE TABLE qrtz_cron_triggers (
    trigger_name character varying(200) NOT NULL,
    trigger_group character varying(200) NOT NULL,
    cron_expression character varying(120) NOT NULL,
    time_zone_id character varying(80)
);


ALTER TABLE public.qrtz_cron_triggers OWNER TO renfe;

--
-- TOC entry 181 (class 1259 OID 517746)
-- Name: qrtz_fired_triggers; Type: TABLE; Schema: public; Owner: renfe; Tablespace: 
--

CREATE TABLE qrtz_fired_triggers (
    entry_id character varying(95) NOT NULL,
    trigger_name character varying(200) NOT NULL,
    trigger_group character varying(200) NOT NULL,
    is_volatile boolean NOT NULL,
    instance_name character varying(200) NOT NULL,
    fired_time bigint NOT NULL,
    priority integer NOT NULL,
    state character varying(16) NOT NULL,
    job_name character varying(200),
    job_group character varying(200),
    is_stateful boolean,
    requests_recovery boolean
);


ALTER TABLE public.qrtz_fired_triggers OWNER TO renfe;

--
-- TOC entry 172 (class 1259 OID 517650)
-- Name: qrtz_job_details; Type: TABLE; Schema: public; Owner: renfe; Tablespace: 
--

CREATE TABLE qrtz_job_details (
    job_name character varying(200) NOT NULL,
    job_group character varying(200) NOT NULL,
    description character varying(250),
    job_class_name character varying(250) NOT NULL,
    is_durable boolean NOT NULL,
    is_volatile boolean NOT NULL,
    is_stateful boolean NOT NULL,
    requests_recovery boolean NOT NULL,
    job_data bytea
);


ALTER TABLE public.qrtz_job_details OWNER TO renfe;

--
-- TOC entry 173 (class 1259 OID 517658)
-- Name: qrtz_job_listeners; Type: TABLE; Schema: public; Owner: renfe; Tablespace: 
--

CREATE TABLE qrtz_job_listeners (
    job_name character varying(200) NOT NULL,
    job_group character varying(200) NOT NULL,
    job_listener character varying(200) NOT NULL
);


ALTER TABLE public.qrtz_job_listeners OWNER TO renfe;

--
-- TOC entry 183 (class 1259 OID 517760)
-- Name: qrtz_locks; Type: TABLE; Schema: public; Owner: renfe; Tablespace: 
--

CREATE TABLE qrtz_locks (
    lock_name character varying(40) NOT NULL
);


ALTER TABLE public.qrtz_locks OWNER TO renfe;

--
-- TOC entry 180 (class 1259 OID 517741)
-- Name: qrtz_paused_trigger_grps; Type: TABLE; Schema: public; Owner: renfe; Tablespace: 
--

CREATE TABLE qrtz_paused_trigger_grps (
    trigger_group character varying(200) NOT NULL
);


ALTER TABLE public.qrtz_paused_trigger_grps OWNER TO renfe;

--
-- TOC entry 182 (class 1259 OID 517755)
-- Name: qrtz_scheduler_state; Type: TABLE; Schema: public; Owner: renfe; Tablespace: 
--

CREATE TABLE qrtz_scheduler_state (
    instance_name character varying(200) NOT NULL,
    last_checkin_time bigint NOT NULL,
    checkin_interval bigint NOT NULL
);


ALTER TABLE public.qrtz_scheduler_state OWNER TO renfe;

--
-- TOC entry 175 (class 1259 OID 517684)
-- Name: qrtz_simple_triggers; Type: TABLE; Schema: public; Owner: renfe; Tablespace: 
--

CREATE TABLE qrtz_simple_triggers (
    trigger_name character varying(200) NOT NULL,
    trigger_group character varying(200) NOT NULL,
    repeat_count bigint NOT NULL,
    repeat_interval bigint NOT NULL,
    times_triggered bigint NOT NULL
);


ALTER TABLE public.qrtz_simple_triggers OWNER TO renfe;

--
-- TOC entry 178 (class 1259 OID 517720)
-- Name: qrtz_trigger_listeners; Type: TABLE; Schema: public; Owner: renfe; Tablespace: 
--

CREATE TABLE qrtz_trigger_listeners (
    trigger_name character varying(200) NOT NULL,
    trigger_group character varying(200) NOT NULL,
    trigger_listener character varying(200) NOT NULL
);


ALTER TABLE public.qrtz_trigger_listeners OWNER TO renfe;

--
-- TOC entry 174 (class 1259 OID 517671)
-- Name: qrtz_triggers; Type: TABLE; Schema: public; Owner: renfe; Tablespace: 
--

CREATE TABLE qrtz_triggers (
    trigger_name character varying(200) NOT NULL,
    trigger_group character varying(200) NOT NULL,
    job_name character varying(200) NOT NULL,
    job_group character varying(200) NOT NULL,
    is_volatile boolean NOT NULL,
    description character varying(250),
    next_fire_time bigint,
    prev_fire_time bigint,
    priority integer,
    trigger_state character varying(16) NOT NULL,
    trigger_type character varying(8) NOT NULL,
    start_time bigint NOT NULL,
    end_time bigint,
    calendar_name character varying(200),
    misfire_instr smallint,
    job_data bytea
);


ALTER TABLE public.qrtz_triggers OWNER TO renfe;

--
-- TOC entry 171 (class 1259 OID 509360)
-- Name: tweet_publicado; Type: TABLE; Schema: public; Owner: renfe; Tablespace: 
--

CREATE TABLE tweet_publicado (
    id numeric NOT NULL,
    id_negocio numeric NOT NULL,
    texto text,
    fecha_publicacion timestamp without time zone
);


ALTER TABLE public.tweet_publicado OWNER TO renfe;

--
-- TOC entry 2039 (class 0 OID 509326)
-- Dependencies: 170
-- Data for Name: cuenta_twitter; Type: TABLE DATA; Schema: public; Owner: renfe
--

INSERT INTO cuenta_twitter VALUES (10, 'Comunidad Madrid', 'Castellano', 'pPbjvlR8Rpf31xtaX9gvG53R9', 'hzTYfPcoPwRa5zZwdgzK1259RTPAGpA8n6eVIFA9BYIcJYhs6T', '3045074446-DL9aDCNefi9uEZZ5PyZw74JnNaRTAZfMlWguP4W', '9IaZ1UTLSJsUAPOONwRQdu5mFaMqSnabjMcpNVUAJVWME', 'MAD');
INSERT INTO cuenta_twitter VALUES (40, 'Comunidad Valenciana', 'Valenciano', 'pPbjvlR8Rpf31xtaX9gvG53R9', 'hzTYfPcoPwRa5zZwdgzK1259RTPAGpA8n6eVIFA9BYIcJYhs6T', '3045074446-DL9aDCNefi9uEZZ5PyZw74JnNaRTAZfMlWguP4W', '9IaZ1UTLSJsUAPOONwRQdu5mFaMqSnabjMcpNVUAJVWME', 'CVA');
INSERT INTO cuenta_twitter VALUES (50, 'Barcelona', 'Catalan', 'pPbjvlR8Rpf31xtaX9gvG53R9', 'hzTYfPcoPwRa5zZwdgzK1259RTPAGpA8n6eVIFA9BYIcJYhs6T', '3045074446-DL9aDCNefi9uEZZ5PyZw74JnNaRTAZfMlWguP4W', '9IaZ1UTLSJsUAPOONwRQdu5mFaMqSnabjMcpNVUAJVWME', 'BAR');
INSERT INTO cuenta_twitter VALUES (60, 'Bilbao', 'Euskera', 'pPbjvlR8Rpf31xtaX9gvG53R9', 'hzTYfPcoPwRa5zZwdgzK1259RTPAGpA8n6eVIFA9BYIcJYhs6T', '3045074446-DL9aDCNefi9uEZZ5PyZw74JnNaRTAZfMlWguP4W', '9IaZ1UTLSJsUAPOONwRQdu5mFaMqSnabjMcpNVUAJVWME', 'BIL');


--
-- TOC entry 2046 (class 0 OID 517707)
-- Dependencies: 177
-- Data for Name: qrtz_blob_triggers; Type: TABLE DATA; Schema: public; Owner: renfe
--



--
-- TOC entry 2048 (class 0 OID 517733)
-- Dependencies: 179
-- Data for Name: qrtz_calendars; Type: TABLE DATA; Schema: public; Owner: renfe
--



--
-- TOC entry 2045 (class 0 OID 517694)
-- Dependencies: 176
-- Data for Name: qrtz_cron_triggers; Type: TABLE DATA; Schema: public; Owner: renfe
--



--
-- TOC entry 2050 (class 0 OID 517746)
-- Dependencies: 181
-- Data for Name: qrtz_fired_triggers; Type: TABLE DATA; Schema: public; Owner: renfe
--



--
-- TOC entry 2041 (class 0 OID 517650)
-- Dependencies: 172
-- Data for Name: qrtz_job_details; Type: TABLE DATA; Schema: public; Owner: renfe
--

INSERT INTO qrtz_job_details VALUES ('jobDetail', 'DEFAULT', NULL, 'es.renfe.ift.job.GenericQuartzJob', false, false, false, false, '\x230d0a23547565204d61722032342031313a35313a34382043455420323031350d0a626174636850726f636573736f724e616d653d6d7952756e6e61626c654a6f620d0a');


--
-- TOC entry 2042 (class 0 OID 517658)
-- Dependencies: 173
-- Data for Name: qrtz_job_listeners; Type: TABLE DATA; Schema: public; Owner: renfe
--



--
-- TOC entry 2052 (class 0 OID 517760)
-- Dependencies: 183
-- Data for Name: qrtz_locks; Type: TABLE DATA; Schema: public; Owner: renfe
--

INSERT INTO qrtz_locks VALUES ('TRIGGER_ACCESS');
INSERT INTO qrtz_locks VALUES ('JOB_ACCESS');
INSERT INTO qrtz_locks VALUES ('CALENDAR_ACCESS');
INSERT INTO qrtz_locks VALUES ('STATE_ACCESS');
INSERT INTO qrtz_locks VALUES ('MISFIRE_ACCESS');
```
