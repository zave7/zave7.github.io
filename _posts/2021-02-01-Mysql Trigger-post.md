---
title: "MariaDB Trigger"
categories: MariaDB
---

# MariaDB Trigger

## INSERT
```
DELIMITER $$

USE `testdb`$$

DROP TRIGGER IF EXISTS `TEST_after_insert`$$

CREATE TRIGGER `TEST_after_insert` AFTER INSERT ON `TEST_TABLE`
	FOR EACH ROW BEGIN
		INSERT INTO `RESULT_TABLE` (created_date, count) 
		VALUES (DATE_FORMAT(NEW.created_date, '%Y%m%d')
					, NEW.count);
	END;

$$
```

## UPDATE
```
DELIMITER $$

USE `testdb`$$

DROP TRIGGER IF EXISTS `TEST_after_update`$$

CREATE TRIGGER `TEST_after_update` AFTER UPDATE ON `TEST_TABLE`
	FOR EACH ROW BEGIN
    UPDATE `RESULT_TABLE`
    SET count = NEW.count + 1
    WHERE created_date = DATE_FORMAT(NEW.created_date, '%Y%m%d');
	END;

$$
```
