# Chess-Tournament
Description of the Project: This is the Chess Database Project that I created in my Database foundations class. 

**ZUMA International Chess Organization**
My organization has sub branch in many countries and its HQ is in Dallas. The club always accepts new players and their chess clubs. At the beginning of the every May, I am starting a new tournament and all clubs must have a participant to attend. After the tournament is done, rankings will be posted on your club web site.  


BUAN 6320.002 IPA-3
1
BUAN 6320.002
CHESS TOURNAMENT PROJECT
INDIVIDUAL PROJECT ASSIGNMENT MILESTONE-3
05/12/21
Prepared by
Nitika Sharma
Net ID: NXS200013
Under the guidance of
Prof Engin Calisr
BUAN 6320.002 IPA-3
2
INDEX
CREATING THE DATABASE------------------------------------------------------------------------3
CREATING THE TABLES-----------------------------------------------------------------------------3
INSERTING THE VALUES IN THE TABLE-------------------------------------------------------5
INNER JOIN---------------------------------------------------------------------------------------------10
FULL JOIN-----------------------------------------------------------------------------------------------11
LEFT OUTER JOIN------------------------------------------------------------------------------------11
RIGHT OUTER JOIN----------------------------------------------------------------------------------12
INTERSECT --------------------------------------------------------------------------------------------13
UNION----------------------------------------------------------------------------------------------------13
EXCEPT--------------------------------------------------------------------------------------------------13
ERD-------------------------------------------------------------------------------------------------------14
CODES----------------------------------------------------------------------------------------------------15
BUAN 6320.002 IPA-3
3
1) Creating the Chess Database:
SQL Commands:
Create database Chessdatabase;
use Chessdatabase;
2) Creating the Tables:
I have created 8 Tables which are as following: Ranking Table, Tournament Table, Chess_Club Table, Player Table, Refree Table, Result Table, Match Table, Sponsor Table.
RANKING TABLE:In ranking table the PK is Ranking_ID.
CREATE TABLE Ranking
(
Ranking_ID VARCHAR(15) NOT NULL UNIQUE,
Rank_description VARCHAR(15) NOT NULL,
CONSTRAINT pk_Ranking PRIMARY KEY (Ranking_Id)
);
TOURNAMENT TABLE: In Tournament table the PK is Tournament_ID.
CREATE TABLE Tournament
(
Tournament_ID VARCHAR(15) NOT NULL UNIQUE,
Tournament_Name VARCHAR(15) NOT NULL,
Tournament_Year VARCHAR(15) NOT NULL,
CONSTRAINT pk_Tournament PRIMARY KEY (Tournament_ID)
);
CHESS CLUB TABLE: In Chess Club table the PK is Club_ID and FK is Tournament_ID
CREATE TABLE Chess_Club
(
Club_ID VARCHAR(15) NOT NULL UNIQUE,
Club_Name VARCHAR(15) NOT NULL,
CONSTRAINT pk_Chess_Club PRIMARY KEY (Club_id ),
BUAN 6320.002 IPA-3
4
Tournament_ID VARCHAR(15) NOT NULL REFERENCES Tournament(Tournament_ID),
);
PLAYER TABLE In Player table the PK is Player_ID and FK are Ranking_ID, Club_ID
CREATE TABLE Player
(
Player_ID VARCHAR(15) NOT NULL UNIQUE,
Ranking_ID VARCHAR(15) NOT NULL REFERENCES Ranking(Ranking_ID),
Club_ID VARCHAR(15) NOT NULL REFERENCES Chess_Club(Club_id),
Player_FirstName VARCHAR(15) NOT NULL,
Player_LastName VARCHAR(15) NOT NULL,
Player_Address VARCHAR(100) ,
CONSTRAINT pk_Player PRIMARY KEY (Player_ID)
);
SPONSORS TABLE In Sponsors table the PK is Sponsor_ID and FK is Club_ID
CREATE TABLE Sponsors
(
Sponsors_ID VARCHAR(15) NOT NULL UNIQUE,
Club_ID VARCHAR(15) NOT NULL REFERENCES Chess_Club(Club_id ),
Sponsor_Name VARCHAR(15) NOT NULL,
Sponsor_Address VARCHAR(100) ,
Sponsor_PhoneNumber VARCHAR(15) ,
CONSTRAINT pk_Sponsors PRIMARY KEY (Sponsors_ID )
);
REFREE TABLE In Refree table the PK is Refree_ID.
CREATE TABLE Refree
(
Refree_ID VARCHAR(15) NOT NULL UNIQUE,
Refree_FirstName VARCHAR(15) NOT NULL,
Refree_LastName VARCHAR(15) ,
Refree_Address VARCHAR(100)NOT NULL ,
CONSTRAINT pk_Refree PRIMARY KEY (Refree_ID )
BUAN 6320.002 IPA-3
5
);
RESULT TABLE In Result table the PK is Result_ID.
CREATE TABLE Result
(
Result_ID VARCHAR(15) NOT NULL UNIQUE,
Result_description VARCHAR(15) NOT NULL,
CONSTRAINT pk_Result PRIMARY KEY (Result_ID )
);
MATCH TABLE In Match table the PK is Surr_ID(Surrogate Key) and FK are Tournament_ID, Refree_ID, Result_ID.
CREATE TABLE Match
(
Surr_ID VARCHAR (15) NOT NULL UNIQUE,
Match_ID VARCHAR(15) NOT NULL,
Tournament_ID VARCHAR(15) NOT NULL REFERENCES Tournament(Tournament_ID ),
Refree_ID VARCHAR(15) NOT NULL REFERENCES Refree( Refree_ID),
Result_ID VARCHAR(15) NOT NULL REFERENCES Result(Result_ID),
Match_Name VARCHAR(15),
CONSTRAINT pk_Surr PRIMARY KEY (Surr_ID)
);
3) Inserting the values in the tables :
Inserting the values in RANKING TABLE and SELECTING ALL:
INSERT INTO Ranking VALUES('X0001','1');
INSERT INTO Ranking VALUES('X0002','2');
INSERT INTO Ranking VALUES('X0003','3');
INSERT INTO Ranking VALUES('X0004','4');
INSERT INTO Ranking VALUES('X0005','5');
INSERT INTO Ranking VALUES('X0006','6');
INSERT INTO Ranking VALUES('X0007','7');
INSERT INTO Ranking VALUES('X0008','8');
SELECT * FROM Ranking;
BUAN 6320.002 IPA-3
6
Inserting the values in TOURNAMENT TABLE and SELECTING ALL:
INSERT INTO Tournament VALUES('101','Prodigies','2019');
INSERT INTO Tournament VALUES('102','Avengers', '2020');
SELECT * FROM Tournament;
Inserting the values in CHESS CLUB TABLE and SELECTING ALL:
INSERT INTO Chess_Club VALUES('A','Rook','101');
INSERT INTO Chess_Club VALUES('B', 'Bishop', '101');
INSERT INTO Chess_Club VALUES('C', 'Checkmate', '101');
INSERT INTO Chess_Club VALUES('D', 'Gambit', '101');
SELECT * FROM Chess_Club;
BUAN 6320.002 IPA-3
7
Inserting the values in PLAYER TABLE and SELECTING ALL:
INSERT INTO Player VALUES('A01','X0001','A','Derek','Smith','711-2880 Nulla St. Mankato Mississippi 96522');
INSERT INTO Player VALUES('A02','X0002', 'A', 'Emma','Jean','606-3727 Ullamcorper. Street Roseville NH 11523');
INSERT INTO Player VALUES('A03','X0003', 'B', 'William','Drey','7050 South Boston St. Methuen, MA 01844');
INSERT INTO Player VALUES('A04','X0004', 'C', 'Ava','Reed','9634 Wilson St. West Palm Beach, FL 33404');
INSERT INTO Player VALUES('A05','X0005', 'C', 'Cory','Freeman', '33 Pineknoll Ave. Dallas, TX 75211');
INSERT INTO Player VALUES('A06','X0006', 'B','John','Hanks',NULL);
INSERT INTO Player VALUES('A07','X0007', 'D','Morgan','Bale','467 Grant Dr. Astoria, NY 11103');
INSERT INTO Player VALUES('A08','X0008', 'D', 'Robert', 'Pitt','9570 Oakwood St. Webster, NY 14580');
SELECT * FROM Player;
Inserting the values in SPONSORS TABLE and SELECTING ALL:
INSERT INTO Sponsors VALUES('S0001', 'A', 'Honda', '1919 Torrance Boulevard Torrance CA 90501-2746 USA','209-200-6239');
INSERT INTO Sponsors VALUES('S0002', 'A','Dell', 'One Dell Way Round Rock, Texas 78682', '316-754-5323');
BUAN 6320.002 IPA-3
8
INSERT INTO Sponsors VALUES('S0003','A','Coco-Cola' ,NULL,'250 375-9756');
INSERT INTO Sponsors VALUES('S0004', 'B', 'Red Bull', '1455 Market St. in San Francisco, California.', NULL);
INSERT INTO Sponsors VALUES('S0005', 'C', 'Acer', '410 Terry Ave. North Seattle WA 98109-5210', '211 313-2647');
INSERT INTO Sponsors VALUES('S0006', 'C', 'Microsoft','410 Terry Ave. North Seattle WA, 98109-5210','212 233-4642');
INSERT INTO Sponsors VALUES('S0007', 'D', 'HBO',NULL, NULL);
SELECT * FROM Sponsors;
Inserting the values in REFREE TABLE and SELECTING ALL:
INSERT INTO Refree VALUES('1A1','June', 'Cole','8752 West Arrowhead Drive New York NY 10034');
INSERT INTO Refree VALUES('1A2','Jennifer','Rule','8059 Littleton Circle Oklahoma City OK 73139');
INSERT INTO Refree VALUES('1A3','Chen','Zhing','789 Glenwood Dr. Oklahoma City OK 73104');
INSERT INTO Refree VALUES('1A4','Veni','Sharma', '4 Rosewood St. Bethany, OK 73008');
INSERT INTO Refree VALUES('1A5','Amen', NULL , 'St. Bethany, OK 73008');
INSERT INTO Refree VALUES('1A6','David', 'Kim', 'Arrowhead Drive New York NY 10034');
SELECT * FROM Refree;
BUAN 6320.002 IPA-3
9
Inserting the values in RESULT TABLE and SELECTING ALL:
INSERT INTO Result VALUES('AAW','Won');
INSERT INTO Result VALUES('AAL','Lost');
SELECT * FROM Result;
Inserting the values in MATCH TABLE and SELECTING ALL:
INSERT INTO Match VALUES( '1001', 'A1','101','1A1','AAW','Match A1');
INSERT INTO Match VALUES('1002','A1','101', '1A1','AAL', NULL);
INSERT INTO Match VALUES('1003','A5','101','1A1','AAW','Match A5');
INSERT INTO Match VALUES('1004','A7','101','1A3','AAW', 'Match A7');
INSERT INTO Match VALUES('1005','B1','102','1A1','AAW', NULL);
INSERT INTO Match VALUES('1006','B2','102','1A2','AAW','Match B2');
INSERT INTO Match VALUES('1007','A2','101','1A2','AAW', 'Match A2');
INSERT INTO Match VALUES('1008','A3','101','1A3','AAL','Match A3');
INSERT INTO Match VALUES('1009','A5','101','1A1','AAL','Match A5');
INSERT INTO Match VALUES('1010','B1','102','1A1','AAL','Match B1');
INSERT INTO Match VALUES('1011','B3','102','1A3','AAL','Match B3');
INSERT INTO Match VALUES('1012','A2','101','1A2','AAL','Match A2');
INSERT INTO Match VALUES('1013','A3','101','1A3','AAW', 'Match A3');
INSERT INTO Match VALUES('1011','A6','101','1A2','AAW','Match A6');
INSERT INTO Match VALUES('1012','A7','101','1A3','AAL','Match A7');
INSERT INTO Match VALUES('1013','B2','102','1A2','AAL','Match B2');
INSERT INTO Match VALUES('1014','B3','102','1A3','AAW', NULL);
INSERT INTO Match VALUES('1015','A4','101','1A4','AAW','Match A4');
INSERT INTO Match VALUES('1016','A4','101','1A4','AAL', NULL);
INSERT INTO Match VALUES('1017','A6','101','1A2','AAL', 'Match A6');
INSERT INTO Match VALUES('1018','B4','102','1A4','AAW','Match B4');
INSERT INTO Match VALUES('1019','B4','102','1A4','AAL', NULL);
SELECT * FROM Match ;
BUAN 6320.002 IPA-3
10
4) INNER JOIN
Create inner joins between two tables and explain what is the purpose of your join?
Purpose: The purpose of creating this INNER JOIN is to check the Players with top 3 Ranks from Players and Ranking tables.
SELECT r.Rank_description, p.Player_FirstName, p.Player_LastName, r.Ranking_ID, p.Player_ID
from Player p
INNER JOIN Ranking r
ON p.Ranking_ID = r.Ranking_ID
WHERE r.Rank_description < 4
BUAN 6320.002 IPA-3
11
5) FULL JOIN:
Create full joins between two tables and explain what is the purpose of your join?
Purpose: The purpose of creating this FULL JOIN is to find which Refree monitors which Matches from Refree table and Match Table.
SELECT r.Refree_FirstName, r.Refree_LastName, m.Match_Name
from Match m
FULL OUTER JOIN Refree r
ON m.Refree_ID = r.Refree_ID
WHERE Match_Name IS NOT NULL;
6) LEFT OUTER JOIN
Create left outer joins between two tables and explain what is the purpose of your join ?
BUAN 6320.002 IPA-3
12
Purpose: The purpose of creating this LEFT OUTER JOIN is to find the information of the Refrees who don’t monitor matches.
SELECT r.Refree_ID, r.Refree_FirstName, r.Refree_LastName, r.Refree_Address, m.Surr_ID
from Refree r
LEFT OUTER JOIN Match m
ON r.Refree_ID = m.Refree_ID
WHERE Surr_ID IS NULL;
7) RIGHT OUTER JOIN
Create right outer joins between two tables and explain what is the purpose of your join ?
Purpose: The purpose of creating this RIGHT OUTER JOIN is to find the Names of the Clubs sponsored by different sponsors from Chess_Club and Sponsor table
SELECT s.Sponsor_Name, c.Club_Name
from Sponsors s
RIGHT OUTER JOIN Chess_Club c
ON s.Club_ID = c.Club_ID;
BUAN 6320.002 IPA-3
13
8) INTERSECT
Create intersect between two tables and explain what is the purpose of your intersect?
Purpose: The purpose of creating this INTERSECT is to Count all the refrees who monitor the matches. Not all refree monitor the matches. Only 4 Refrees out of the 6 Refrees monitor the matches. Rest 2 refrees don’t monitor the matches
SELECT COUNT(*) FROM
(
SELECT Refree_ID FROM Match
INTERSECT
SELECT Refree_ID FROM Refree
)I
9) UNION
Create a union between two tables and explain what is the purpose of your union?
Purpose: The purpose of creating this UNION is to get all the Club IDs which are sponsored by sponsors.
SELECT Club_ID FROM Sponsors
UNION
SELECT Club_ID FROM Chess_Club;
10) EXCEPT
BUAN 6320.002 IPA-3
14
Create except between two tables and explain what is the purpose of your except?
Purpose: The purpose of creating this EXCEPT is to get refree ID who don’t monitor any matches.
SELECT Refree_ID FROM Refree
EXCEPT
SELECT Refree_ID FROM Match
11) ERD
BUAN 6320.002 IPA-3
15
12) Codes:
Create database Chessdatabase;
use Chessdatabase;
-----------------------CREATE RANKING TABLE---------------------------
CREATE TABLE Ranking
(
Ranking_ID VARCHAR(15) NOT NULL UNIQUE,
Rank_description VARCHAR(15) NOT NULL,
CONSTRAINT pk_Ranking PRIMARY KEY (Ranking_Id)
);
INSERT INTO Ranking VALUES('X0001','1');
INSERT INTO Ranking VALUES('X0002','2');
INSERT INTO Ranking VALUES('X0003','3');
INSERT INTO Ranking VALUES('X0004','4');
INSERT INTO Ranking VALUES('X0005','5');
INSERT INTO Ranking VALUES('X0006','6');
INSERT INTO Ranking VALUES('X0007','7');
INSERT INTO Ranking VALUES('X0008','8');
SELECT * FROM Ranking;
-----------------------CREATE TOURNAMENT TABLE---------------------------
CREATE TABLE Tournament
(
Tournament_ID VARCHAR(15) NOT NULL UNIQUE,
Tournament_Name VARCHAR(15) NOT NULL,
Tournament_Year VARCHAR(15) NOT NULL,
CONSTRAINT pk_Tournament PRIMARY KEY (Tournament_ID)
);
INSERT INTO Tournament VALUES('101','Prodigies','2019');
INSERT INTO Tournament VALUES('102','Avengers', '2020');
SELECT * FROM Tournament;
-----------------------CREATE CHESS CLUB TABLE---------------------------
CREATE TABLE Chess_Club
(
Club_ID VARCHAR(15) NOT NULL UNIQUE,
Tournament_ID VARCHAR(15) NOT NULL REFERENCES Tournament(Tournament_ID),
Club_Name VARCHAR(15) NOT NULL,
CONSTRAINT pk_Chess_Club PRIMARY KEY (Club_id ),
);
INSERT INTO Chess_Club VALUES('A','Rook','101');
INSERT INTO Chess_Club VALUES('B', 'Bishop', '101');
INSERT INTO Chess_Club VALUES('C', 'Checkmate', '101');
INSERT INTO Chess_Club VALUES('D', 'Gambit', '101');
SELECT * FROM Chess_Club;
BUAN 6320.002 IPA-3
16
-----------------------CREATE PLAYER TABLE---------------------------
CREATE TABLE Player
(
Player_ID VARCHAR(15) NOT NULL UNIQUE,
Ranking_ID VARCHAR(15) NOT NULL REFERENCES Ranking(Ranking_ID),
Club_ID VARCHAR(15) NOT NULL REFERENCES Chess_Club(Club_id),
Player_FirstName VARCHAR(15) NOT NULL,
Player_LastName VARCHAR(15) NOT NULL,
Player_Address VARCHAR(100) ,
CONSTRAINT pk_Player PRIMARY KEY (Player_ID)
);
INSERT INTO Player VALUES('A01','X0001','A','Derek','Smith','711-2880 Nulla St. Mankato Mississippi 96522');
INSERT INTO Player VALUES('A02','X0002', 'A', 'Emma','Jean','606-3727 Ullamcorper. Street Roseville NH 11523');
INSERT INTO Player VALUES('A03','X0003', 'B', 'William','Drey','7050 South Boston St. Methuen, MA 01844');
INSERT INTO Player VALUES('A04','X0004', 'C', 'Ava','Reed','9634 Wilson St. West Palm Beach, FL 33404');
INSERT INTO Player VALUES('A05','X0005', 'C', 'Cory','Freeman', '33 Pineknoll Ave. Dallas, TX 75211');
INSERT INTO Player VALUES('A06','X0006', 'B','John','Hanks',NULL);
INSERT INTO Player VALUES('A07','X0007', 'D','Morgan','Bale','467 Grant Dr. Astoria, NY 11103');
INSERT INTO Player VALUES('A08','X0008', 'D', 'Robert', 'Pitt','9570 Oakwood St. Webster, NY 14580');
SELECT * FROM Player;
-----------------------CREATE SPONSORS TABLE---------------------------
CREATE TABLE Sponsors
(
Sponsors_ID VARCHAR(15) NOT NULL UNIQUE,
Club_ID VARCHAR(15) NOT NULL REFERENCES Chess_Club(Club_id ),
Sponsor_Name VARCHAR(15) NOT NULL,
Sponsor_Address VARCHAR(100) ,
Sponsor_PhoneNumber VARCHAR(15) ,
CONSTRAINT pk_Sponsors PRIMARY KEY (Sponsors_ID )
);
INSERT INTO Sponsors VALUES('S0001', 'A', 'Honda', '1919 Torrance Boulevard Torrance CA 90501-2746 USA','209-200-6239');
INSERT INTO Sponsors VALUES('S0002', 'A','Dell','One Dell Way Round Rock, Texas 78682', '316-754-5323');
INSERT INTO Sponsors VALUES('S0003','A','Coco-Cola' ,NULL,'250 375-9756');
INSERT INTO Sponsors VALUES('S0004', 'B', 'Red Bull', '1455 Market St. in San Francisco, California.', NULL);
INSERT INTO Sponsors VALUES('S0005', 'C', 'Acer', '410 Terry Ave. North Seattle WA 98109-5210', '211 313-2647');
INSERT INTO Sponsors VALUES('S0006', 'C', 'Microsoft','410 Terry Ave. North Seattle WA, 98109-5210','212 233-4642');
INSERT INTO Sponsors VALUES('S0007', 'D', 'HBO',NULL, NULL);
SELECT * FROM Sponsors;
BUAN 6320.002 IPA-3
17
-----------------------CREATE REFREE TABLE---------------------------
CREATE TABLE Refree
(
Refree_ID VARCHAR(15) NOT NULL UNIQUE,
Refree_FirstName VARCHAR(15) NOT NULL,
Refree_LastName VARCHAR(15) ,
Refree_Address VARCHAR(100)NOT NULL ,
CONSTRAINT pk_Refree PRIMARY KEY (Refree_ID )
);
INSERT INTO Refree VALUES('1A1','June', 'Cole', '8752 West Arrowhead Drive New York NY 10034');
INSERT INTO Refree VALUES('1A2','Jennifer', 'Rule', '8059 Littleton Circle Oklahoma City OK 73139');
INSERT INTO Refree VALUES('1A3','Chen', 'Zhing', '789 Glenwood Dr. Oklahoma City OK 73104');
INSERT INTO Refree VALUES('1A4','Veni', 'Sharma','4 Rosewood St. Bethany, OK 73008');
INSERT INTO Refree VALUES('1A5','Amen', NULL , 'St. Bethany, OK 73008');
INSERT INTO Refree VALUES('1A6','David','Kim', 'Arrowhead Drive New York NY 10034');
SELECT * FROM Refree;
-----------------------CREATE RESULT TABLE---------------------------
CREATE TABLE Result
(
Result_ID VARCHAR(15) NOT NULL UNIQUE,
Result_description VARCHAR(15) NOT NULL,
CONSTRAINT pk_Result PRIMARY KEY (Result_ID )
);
INSERT INTO Result VALUES('AAW','Won');
INSERT INTO Result VALUES('AAL','Lost');
SELECT * FROM Result;
-----------------------CREATE MATCH TABLE---------------------------
CREATE TABLE Match
(
Surr_ID VARCHAR (15) NOT NULL UNIQUE,
Match_ID VARCHAR(15) NOT NULL,
Tournament_ID VARCHAR(15) NOT NULL REFERENCES Tournament(Tournament_ID ),
Refree_ID VARCHAR(15) NOT NULL REFERENCES Refree( Refree_ID),
Result_ID VARCHAR(15) NOT NULL REFERENCES Result(Result_ID),
Match_Name VARCHAR(15),
CONSTRAINT pk_Surr PRIMARY KEY (Surr_ID)
);
INSERT INTO Match VALUES( '1001', 'A1','101','1A1','AAW','Match A1');
INSERT INTO Match VALUES('1002','A1','101', '1A1','AAL', NULL);
INSERT INTO Match VALUES('1003','A5','101','1A1','AAW','Match A5');
INSERT INTO Match VALUES('1004','A7','101','1A3','AAW', 'Match A7');
INSERT INTO Match VALUES('1005','B1','102','1A1','AAW', NULL);
INSERT INTO Match VALUES('1006','B2','102','1A2','AAW','Match B2');
INSERT INTO Match VALUES('1007','A2','101','1A2','AAW', 'Match A2');
INSERT INTO Match VALUES('1008','A3','101','1A3','AAL','Match A3');
INSERT INTO Match VALUES('1009','A5','101','1A1','AAL','Match A5');
INSERT INTO Match VALUES('1010','B1','102', '1A1','AAL','Match B1');
BUAN 6320.002 IPA-3
18
INSERT INTO Match VALUES('1011','B3','102', '1A3','AAL','Match B3');
INSERT INTO Match VALUES('1012','A2','101', '1A2','AAL','Match A2');
INSERT INTO Match VALUES('1013','A3','101','1A3','AAW', 'Match A3');
INSERT INTO Match VALUES('1011','A6','101','1A2','AAW','Match A6');
INSERT INTO Match VALUES('1012','A7','101', '1A3','AAL','Match A7');
INSERT INTO Match VALUES('1013','B2','102', '1A2','AAL','Match B2');
INSERT INTO Match VALUES('1014','B3','102','1A3','AAW', NULL);
INSERT INTO Match VALUES('1015','A4','101', '1A4','AAW','Match A4');
INSERT INTO Match VALUES('1016','A4','101', '1A4','AAL', NULL);
INSERT INTO Match VALUES('1017','A6','101','1A2','AAL', 'Match A6');
INSERT INTO Match VALUES('1018','B4','102', '1A4','AAW','Match B4');
INSERT INTO Match VALUES('1019','B4','102', '1A4','AAL', NULL);
SELECT * FROM Match ;
-----------------------------------------------------------------------------------
----- INNER JOIN between players and Ranks. Top 3 players with ranks top 3--------
SELECT r.Rank_description, p.Player_FirstName, p.Player_LastName, r.Ranking_ID, p.Player_ID
from Player p
INNER JOIN Ranking r
ON p.Ranking_ID = r.Ranking_ID
WHERE r.Rank_description < 4
------------FULL OUTER JOIN Refrees monitor which matches -------------
SELECT r.Refree_FirstName, r.Refree_LastName, m.Match_Name
from Match m
FULL OUTER JOIN Refree r
ON m.Refree_ID = r.Refree_ID
WHERE Match_Name IS NOT NULL;
------------RIGHT JOIN sponsors sponsor which clubs-------------
SELECT s.Sponsor_Name, c.Club_Name
from Sponsors s
RIGHT OUTER JOIN Chess_Club c
ON s.Club_ID = c.Club_ID;
------------LEFT OUTER JOIN Information of the Refrees who don't monitor the matches--------------------
SELECT r.Refree_ID, r.Refree_FirstName, r.Refree_LastName, r.Refree_Address, m.Surr_ID
from Refree r
LEFT OUTER JOIN Match m
ON r.Refree_ID = m.Refree_ID
WHERE Surr_ID IS NULL;
------------UNION getting all the club IDs which are sponsored by sponsors-------------
SELECT Club_ID FROM Sponsors
UNION
SELECT Club_ID FROM Chess_Club;
------------------INTERSECT All the matches have been checked by how many refrees?
SELECT COUNT(*) FROM
BUAN 6320.002 IPA-3
19
(
SELECT Refree_ID FROM Match
INTERSECT
SELECT Refree_ID FROM Refree
)I
--------------- EXCEPT- Are there any refree who didn't monitored Match? How many?
SELECT Refree_ID FROM Refree
EXCEPT
SELECT Refree_ID FROM Match
