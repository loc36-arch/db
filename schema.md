The system shall have two databases (dbs): "EMF STATE" and "COMING SOON".

The "EMF STATE" db shall contain information related to EMF states of sensors, while the "COMING SOON"
db shall contain information related to things coming soon to the platform.

### "EMF STATE" database schema

CREATE TABLE sensor (
	record_id    TEXT  PRIMARY KEY,
	sensor_id    TEXT  NOT NULL  UNIQUE,
	pass         TEXT  NOT NULL,
	some_comment TEXT  NOT NULL
);

CREATE TABLE state (
	record_id  TEXT  PRIMARY KEY,
	state      TEXT  NOT NULL,	
	-- Format: YYYYMMDD
	day        TEXT  NOT NULL,
	-- Format: HHMM
	time       TEXT  NOT NULL,
	sensor     TEXT  NOT NULL,
	FOREIGN KEY sensor REFERENCES sensor.sensor_id
);

CREATE TABLE location (
	record_id  TEXT  PRIMARY KEY,
	id         TEXT  NOT NULL  UNIQUE,
	name       TEXT  NOT NULL  UNIQUE,
	sensor     TEXT  NOT NULL,
	FOREIGN KEY sensor REFERENCES sensor.sensor_id
);

### "COMING SOON" database schema

CREATE TABLE coming_soon (
	record_id   TEXT              PRIMARY KEY,
	message_id  TEXT              NOT NULL  UNIQUE,
	title       TEXT              NOT NULL,
	message     TEXT              NOT NULL,
	image       VARBINARY (8192)  NOT NULL,
	image_mime  TEXT              NOT NULL
);
