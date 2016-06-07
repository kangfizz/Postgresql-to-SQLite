# Postgresql-to-SQLite
This topic is talking about how to move your postgresql table and data to your SQLite database.
##中文說明:此部分為將postgresql放入sqlite資料庫裏面。

##所需物品or工具:  
1.Sublime Text3  
2.test3.sql(要做修改)  
(可以使用test7.sql即可,就不用做STEP.1)  
3.作業系統為linux  

###STEP1:  
打開Sublime Text  
對test3.sql做修改,以下為需要修改 
####A.因為sqlite不會讀COMMENT以及後面的E,所以要把他們全部去掉  
 用Sublime裡面,crtl+H(取代) 將" E' "取代為 " ' "  
####B.對創建TABLE指令做更動:  
 CREATE TABLE IF NOT EXISTS...那邊去除 "COMMENT" 跟 " ' ' "    
並且在最後加入CONSTRAINT navi_address_pk PRIMARY KEY ("id")
####C.因為SQLite有一次輸入500筆的限制,所以我將insert分開  
 a.將" INSERT INTO "navi_address" ("id", "name", "shortname", "eng_name", "subbranch", "address", "tel", "towncode", "poi_no", "fax", "zipcode", "internet", "time", "card", "liaison", "businessmo", "annotation", "croad_id", "along", "colx", "coly", "croad_auto", "keyword") VALUES " 取代為 " "  
 b.將" ( "取代為 "  INSERT INTO "navi_address" ("id", "name", "shortname", "eng_name", "subbranch", "address", "tel", "towncode", "poi_no", "fax", "zipcode", "internet", "time", "card", "liaison", "businessmo", "annotation", "croad_id", "along", "colx", "coly", "croad_auto", "keyword") VALUES ( "  
c.將 " ), "取代為 " ); "  

####D.在Insert前加入"BEGIN;",最尾端加入"COMMIT;" 以此加快速度   

###STEP2:  
####直接放入Sqlite資料庫裏面  
進入sqlite資料庫:sqlite3 dbname.sqlite3  
(dbname此時為db,所以這時候應該是**sqlite3 db.sqlite3**)  
進入後,輸入**.read /home/jerry/test7.sql** (我放test7.sql的位置為/home/jerry)  
等一下時間即可成功(大概3~5分)  
最後可以用**SELECT name FROM navi_address WHERE keyword='0';**  檢查
