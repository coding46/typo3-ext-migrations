# Migrate with doctrine migrations

__It's strongly recommend to use typo3_console!__

Otherwise you can use the TYPO3 built in `cli`.

```
typo3/cli_dispatch.phpsh extbase doctrine:migrate
```

to get the status of your migration you can run:

```
typo3/cli_dispatch.phpsh extbase doctrine:status
```

this will give you an output like that:

```

 == Configuration
    >> Name:                                               Doctrine Database Migrations
    >> Database Driver:                                    pdo_mysql
    >> Database Name:                                      schulcms
    >> Configuration Source:                               manually configured
    >> Version Table Name:                                 doctrine_migrationstatus
    >> Migrations Namespace:                               KayStrobach\Migrations\Persistence\Doctrine\Migrations
    >> Migrations Target Directory:                        /Users/kay/Development/SBS.TYPO3/SchulCmsMigration//fileadmin/Migrations
    >> Current Version:                                    0
    >> Latest Version:                                     2014-07-14 18:44:53 (20140714184453)
    >> Executed Migrations:                                0
    >> Available Migrations:                               1
    >> New Migrations:                                     1

 == Migration Versions
    >> 2014-07-14 18:44:53 (20140714184453) migrations                  not migrated

```

This extension uses `doctrine/migrations` to migrate the database tables.

# own migration

Create a folder called `Migrations\Mysql` in your extension and place a file like this in it.
Then you should see it with the status command.
 
```php
<?php
namespace KayStrobach\Migrations\Persistence\Doctrine\Migrations;

use Doctrine\DBAL\Migrations\AbstractMigration,
	Doctrine\DBAL\Schema\Schema;

/**
 * Auto-generated Migration: Please modify to your need!
 *
 * @SuppressWarnings(PHPMD)
 */
class Version20140714184453 extends AbstractMigration {

	/**
	 * @param Schema $schema
	 * @return void
	 */
	public function up(Schema $schema) {
		// this up() migration is autogenerated, please modify it to your needs
		$this->abortIf($this->connection->getDatabasePlatform()->getName() != "mysql");

        $this->addSql("CREATE TABLE test (textfield VARCHAR(40) NOT NULL) DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci ENGINE = InnoDB");
	}

	/**
	 * @param Schema $schema
	 * @return void
	 */
	public function down(Schema $schema) {
		// this down() migration is autogenerated, please modify it to your needs
		$this->abortIf($this->connection->getDatabasePlatform()->getName() != "mysql");

        $this->addSql("Drop Table test");
	}
}
```

# More information

* http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/
* http://docs.doctrine-project.org/projects/doctrine-migrations/en/latest/toc.html