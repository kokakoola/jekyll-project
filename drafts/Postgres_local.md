## Postgres local install
##### Veateade
##### 24.11.2012

Et ma hoolas ei olnud (tutoorial 3 ptk Harjutused soovitab kasutada Heroku Postgresi), paigaldasin hoopis masinasse Postgresi. Üle [Homebrew](http://blog.tquadrado.com/2010/install-postgresql-in-mac-osx-via-homebrew/"install PostgreSQL in Mac OSX via Homebrew"). Aga siin ma jooksin *permissionitega* rappa. Andmebaasi loomiseks

```initdb /usr/local/var/postgres -E utf8```

annab mulle *permission denied* ja et ma ei kavatse sellega hetkel edasi jageleda, märgin siin kirja kui veakoha, kust hiljem edasi vaadata.

Olgu siia märgitud ka teised Homebrew juhtnöörid alustajale:

	Start/Stop PostgreSQL

	If this is your first install, automatically load on login with:
	  mkdir -p ~/Library/LaunchAgents
	  cp /usr/local/Cellar/postgresql/9.2.1/homebrew.mxcl.postgresql.plist ~/Library/LaunchAgents/
	  launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist

	If this is an upgrade and you already have the homebrew.mxcl.postgresql.plist loaded:
	  launchctl unload -w ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist
	  cp /usr/local/Cellar/postgresql/9.2.1/homebrew.mxcl.postgresql.plist ~/Library/LaunchAgents/
	  launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist

	Or start manually with:
	  pg_ctl -D /usr/local/var/postgres -l /usr/local/var/postgres/server.log start

	And stop with:
	  pg_ctl -D /usr/local/var/postgres stop -s -m fast

	Loading Extensions

	By default, Homebrew builds all available Contrib extensions.  To see a list of all
	available extensions, from the psql command line, run:
	  SELECT * FROM pg_available_extensions;

	To load any of the extension names, navigate to the desired database and run:
	  CREATE EXTENSION [extension name];

	For instance, to load the tablefunc extension in the current database, run:
	  CREATE EXTENSION tablefunc;

	For more information on the CREATE EXTENSION command, see:
	  http://www.postgresql.org/docs/9.2/static/sql-createextension.html
	For more information on extensions, see:
	  http://www.postgresql.org/docs/9.2/static/contrib.html

	Other

	Some machines may require provisioning of shared memory:
	  http://www.postgresql.org/docs/9.2/static/kernel-resources.html#SYSVIPC

	To install postgresql (and ossp-uuid) in 32-bit mode:
	   brew install postgresql --32-bit

	If you want to install the postgres gem, including ARCHFLAGS is recommended:
	    env ARCHFLAGS="-arch x86_64" gem install pg

	To install gems without sudo, see the Homebrew wiki.

	