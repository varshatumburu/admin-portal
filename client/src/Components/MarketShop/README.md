Creating tables for market services:

```
CREATE TABLE Shopkeepers(
  SID INT PRIMARY KEY AUTO_INCREMENT,
  username VARCHAR(255) UNIQUE,
  name VARCHAR(255),
  storeID INT UNIQUE,
  phonenumber BIGINT,
  securitypassID VARCHAR(20),
  passexpiry DATE,
  FOREIGN KEY (username) REFERENCES Users(username),
  FOREIGN KEY (storeID) REFERENCES Stores(StoreID));
```

```
CREATE TABLE billrequests(
  breqID INT PRIMARY KEY AUTO_INCREMENT,
  storeID INT,
  amount INT,
  type ENUM('Rent','Electricity','Others'),
  transactionID  VARCHAR(255),
  modeofpayment VARCHAR(100),
  status ENUM('Denied','Accepted','In review','On hold') DEFAULT 'In review',
  FOREIGN KEY (storeID) REFERENCES Stores(storeID));
```

Adding triggers:

```
DELIMITER $$
CREATE TRIGGER insertShopkeeper
AFTER INSERT
ON Users FOR EACH ROW
BEGIN
IF(NEW.RoleID=3) THEN
INSERT INTO shopkeepers(username) VALUES (new.username);
END IF;
END$$
DELIMITER ;
```