The database of this holme system shall be powered by the Maria DB. The DBMS shall manage
two databases:

emf_state and,
coming_soon

The "emf_state" shall contain information related to EMF states, while the "coming_soon"
database shall contain information related to things coming soon to the platform.

### emf_state database schema

CREATE TABLE sensor (
	record_id  TEXT  NOT NULL  UNIUQE PRIMARY KEY,
	sensor_id  TEXT  NOT NULL  UNIUQE,
	password   TEXT  NOT NULL,
	comment    TEXT  NOT NULL
);

CREATE TABLE state (
	record_id  TEXT  NOT NULL  UNIQUE PRIMARY KEY,
	state      TEXT  NOT NULL,	
	-- Format: YYYYMMDD
	day        TEXT  NOT NULL,
	-- Format: HHMM
	time       TEXT  NOT NULL,
	sensor     TEXT  NOT NULL,
	FOREIGN KEY sensor REFERENCES sensor.sensor_id
);

CREATE TABLE location (
	record_id  TEXT  NOT NULL  UNIQUE PRIMARY KEY,
	id         TEXT  NOT NULL  UNIQUE,
	name       TEXT  NOT NULL  UNIQUE,
	sensor     TEXT  NOT NULL,
	FOREIGN KEY sensor REFERENCES sensor.sensor_id
);

### coming_soon database schema

CREATE TABLE coming_soon (
	record_id   TEXT              NOT NULL  UNIQUE PRIMARY KEY,
	message_id  TEXT              NOT NULL  UNIQUE,
	title       TEXT              NOT NULL,
	message     TEXT              NOT NULL,
	image       VARBINARY (8192)  NOT NULL,
	image_mime  TEXT              NOT NULL
);
