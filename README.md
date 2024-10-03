Enter user-name: system
Enter password:
Last Successful login time: Thu Oct 03 2024 15:48:33 +02:00

Connected to:
Oracle Database 21c Express Edition Release 21.0.0.0.0 - Production
Version 21.3.0.0.0

SQL> select name,open_made from v$pdbs;
select name,open_made from v$pdbs
            *
ERROR at line 1:
ORA-00904: "OPEN_MADE": invalid identifier


SQL> select name,open_mode from v$pdbs;

NAME
--------------------------------------------------------------------------------
OPEN_MODE
----------
PDB$SEED
READ ONLY

XEPDB1
READ WRITE

PLSQL_CLASS2024DB
MOUNTED


SQL> select instance_name from v$instance;

INSTANCE_NAME
----------------
xe

SQL> alter session set container = PLSQL_CLASS2024DBL;
ERROR:
ORA-65011: Pluggable database PLSQL_CLASS2024DBL does not exist.


SQL> alter session set conatiner =PLSQL_CLASS2024DB;
alter session set conatiner =PLSQL_CLASS2024DB
                  *
ERROR at line 1:
ORA-02248: invalid option for ALTER SESSION


SQL> ALTER SESSION SET CONTAINER = PLSQL_CLASS2024DB;
ERROR:
ORA-65024: Pluggable database PLSQL_CLASS2024DB is not open.


SQL> ALTER PLUGGABLE DATABASE PLSQL_CLASS2024DB OPEN;
ALTER PLUGGABLE DATABASE PLSQL_CLASS2024DB OPEN
*
ERROR at line 1:
ORA-01031: insufficient privileges


SQL> ALTER SESSION SET CONTAINER = PLSQL_CLASS2024DB;
ERROR:
ORA-65024: Pluggable database PLSQL_CLASS2024DB is not open.


SQL> CONNECT SYS AS SYSDBA
Enter password:
SP2-0306: Invalid option.
Usage: CONN[ECT] [{logon|/|proxy} [AS {SYSDBA|SYSOPER|SYSASM|SYSBACKUP|SYSDG|SYSKM|SYSRAC}] [edition=value]]
where <logon> ::= <username>[/<password>][@<connect_identifier>]
      <proxy> ::= <proxyuser>[<username>][/<password>][@<connect_identifier>]
SQL> ALTER PLUGGABLE DATABASE PLSQL_CLASS2024DB OPEN;
ALTER PLUGGABLE DATABASE PLSQL_CLASS2024DB OPEN
*
ERROR at line 1:
ORA-01031: insufficient privileges


SQL> ALTER PLUGGABLE DATABASE PLSQL_CLASS2024DB OPEN;
ALTER PLUGGABLE DATABASE PLSQL_CLASS2024DB OPEN
*
ERROR at line 1:
ORA-01031: insufficient privileges


SQL> CONNECT / AS SYSDBA
Connected.
SQL> ALTER PLUGGABLE DATABASE PLSQL_CLASS2024DB OPEN;

Pluggable database altered.

SQL> SELECT name, open_mode, restricted FROM v$pdbs WHERE name = 'PLSQL_CLASS2024DB';

NAME
--------------------------------------------------------------------------------
OPEN_MODE  RES
---------- ---
PLSQL_CLASS2024DB
READ WRITE NO


SQL> ALTER SESSION SET CONTAINER = PLSQL_CLASS2024DB;

Session altered.

SQL> CREATE USER ke_plsqlauca identified by password
  2  ;

User created.

SQL> grant all privileges to ke_plsqlauca;

Grant succeeded.

SQL> create pluggable database ke_to_delete_pdb close immediate;
create pluggable database ke_to_delete_pdb close immediate
                                           *
ERROR at line 1:
ORA-00922: missing or invalid option


SQL> CREATE PLUGGABLE DATABASE ke_to_delete_pdb
  2    ADMIN USER pdb_admin IDENTIFIED BY <password>
  3    ;
  ADMIN USER pdb_admin IDENTIFIED BY <password>
                                      *
ERROR at line 2:
ORA-00922: missing or invalid option


SQL> CREATE PLUGGABLE DATABASE ke_to_delete_pdb
  2    ADMIN USER pdb_admin IDENTIFIED BY <password>
  3    FILE_NAME_CONVERT = ('<source_file_path>', '<target_file_path>');
  ADMIN USER pdb_admin IDENTIFIED BY <password>
                                      *
ERROR at line 2:
ORA-00922: missing or invalid option


SQL> CREATE PLUGGABLE DATABASE plsql_class2024db
  2  ADMIN USER ke_plsqlauca IDENTIFIED BY admin
  3  FILE_NAME_CONVERT =('/oracle/oradata/XE/pdbseed/', '/o
racle/oradata/XE/ke_to_delete_pdb/');
CREATE PLUGGABLE DATABASE plsql_class2024db
*
ERROR at line 1:
ORA-65040: operation not allowed from within a pluggable database


SQL> SQL> ALTER SESSION SET CONTAINER=CDB$ROOT;
SP2-0734: unknown command beginning "SQL> ALTER..." - rest of line ignored.
SQL> ALTER SESSION SET CONTAINER=CDB$ROOT;

Session altered.

SQL> CREATE PLUGGABLE DATABASE plsql_class2024db
  2  ADMIN USER ke_plsqlauca IDENTIFIED BY admin
  3  FILE_NAME_CONVERT=('/oracle/oradata/XE/pdbseed/', '/oracle/oradata/XE/ke_to_delete_pdb/');
CREATE PLUGGABLE DATABASE plsql_class2024db
*
ERROR at line 1:
ORA-65012: Pluggable database PLSQL_CLASS2024DB already exists.

     ALTER PLUGGABLE DATABASE plsql_class2024db CLOSE IMMEDIATE;
SQL>
Pluggable database altered.

SQL> ALTER PLUGGABLE DATABASE plsql_class2024db CLOSE IMMEDIATE;
ALTER PLUGGABLE DATABASE plsql_class2024db CLOSE IMMEDIATE
*
ERROR at line 1:
ORA-65020: pluggable database PLSQL_CLASS2024DB already closed


SQL> show pdbs;

    CON_ID CON_NAME                       OPEN MODE  RESTRICTED
---------- ------------------------------ ---------- ----------
         2 PDB$SEED                       READ ONLY  NO
         3 XEPDB1                         READ WRITE NO
         4 PLSQL_CLASS2024DB              MOUNTED
SQL> CREATE PLUGGABLE DATBASE ke_to_delete_pdb
  2  ADMIN USER ke_plsql IDENTIFIED BY admin
  3  FILE_NAME_CONVERT('/oracle/oradata/XE/pdbseed/', '/o
  4
SQL> racle/oradata/XE/ke_to_delete_pdb/');
SP2-0734: unknown command beginning "racle/orad..." - rest of line ignored.
SQL> CREATE PLUGGABLE DATBASE ke_to_delete_pdb
  2    2  ADMIN USER ke_plsql IDENTIFIED BY admin
  3    3  FILE_NAME_CONVERT('C:\ORACLE\ORADATA\XE\PDBSEED\',('C:\ORACLE\ORADATA\XE\PDBSEED\PDBS\ke_to_delete_pdb\');
CREATE PLUGGABLE DATBASE ke_to_delete_pdb
                 *
ERROR at line 1:
ORA-02000: missing DATABASE keyword


SQL> CREATE PLUGGABLE DATABASE ke_to_delete_pdb
  2     ADMIN USER ke_plsql IDENTIFIED BY admin
  3     FILE_NAME_CONVERT=('C:\ORACLE\ORADATA\XE\PDBSEED\', 'C:\ORACLE\ORADATA\XE\PDBSEED\PDBS\ke_to_delete_pdb\');

Pluggable database created.

SQL>
SQL> ALTER PLUGGABLE DATABASE ke_to_delete_pdb CLOSE IMMEDIATE;
ALTER PLUGGABLE DATABASE ke_to_delete_pdb CLOSE IMMEDIATE
*
ERROR at line 1:
ORA-65020: pluggable database KE_TO_DELETE_PDB already closed


SQL> show pdbs;

    CON_ID CON_NAME                       OPEN MODE  RESTRICTED
---------- ------------------------------ ---------- ----------
         2 PDB$SEED                       READ ONLY  NO
         3 XEPDB1                         READ WRITE NO
         4 PLSQL_CLASS2024DB              MOUNTED
         5 KE_TO_DELETE_PDB               MOUNTED
SQL> DROP PLUGGABLE DATABASE ke_to_delete_pdb including DATAFILES;

Pluggable database dropped.

SQL> DROP PLUGGABLE DATABASE ke_to_delete_pdb including DATAFILES;
DROP PLUGGABLE DATABASE ke_to_delete_pdb including DATAFILES
*
ERROR at line 1:
ORA-65011: Pluggable database KE_TO_DELETE_PDB does not exist.


SQL>
SQL> Pluggable database dropped.
SP2-0734: unknown command beginning "Pluggable ..." - rest of line ignored.
SQL> emctl status dbconsole
SP2-0734: unknown command beginning "emctl stat..." - rest of line ignored.
SQL> Show con_name;

CON_NAME
------------------------------
CDB$ROOT
SQL> ALTER SESSION SET CONTAINER =CDB$ROOT;

Session altered.

SQL> SELECT SYS_CONTEXT('USERENV')AS current_container From dual;
SELECT SYS_CONTEXT('USERENV')AS current_container From dual
       *
ERROR at line 1:
ORA-00938: not enough arguments for function


SQL> SELECT SYS_CONTEXT('USERENV', 'CON_NAME') AS current_container FROM dual;

CURRENT_CONTAINER
--------------------------------------------------------------------------------
CDB$ROOT

SQL> ▪ SELECT DBMS_XDB_CONFIG.GETHTTPPORT() AS HTTP_PORT,
SP2-0171: HELP system not available.
SQL> select DBMS_XDB_CONFIG.GETHTTPPORT() AS HTTP-PORT,DBMS_XDB_CONFIG.GETHTTPSPORT() AS HTTPS_PORT FROM dual;
select DBMS_XDB_CONFIG.GETHTTPPORT() AS HTTP-PORT,DBMS_XDB_CONFIG.GETHTTPSPORT() AS HTTPS_PORT FROM dual
                                            *
ERROR at line 1:
ORA-00923: FROM keyword not found where expected


SQL> SELECT DBMS_XDB_CONFIG.GETHTTPPORT() AS HTTP_PORT,
  2         DBMS_XDB_CONFIG.GETHTTPSPORT() AS HTTPS_PORT
  3  FROM dual;

 HTTP_PORT HTTPS_PORT
---------- ----------
         0       5500

SQL> BEGIN
  2  DBMS_XDBS_CONFIG.SETHTTPPORT() AS HTTP_PORT,
  3         DBMS_XDB_CONFIG.GETHTTPSPORT() AS HTTPS_PORT ;
  4  BEGIN
  5  DBMS_XDB_CONFIG.SETHTTPPORT(8080);
  6  DBMS_XDB_CONFIG.SETHTTPSPORT(5500);
  7  END;
  8  /
DBMS_XDBS_CONFIG.SETHTTPPORT() AS HTTP_PORT,
                               *
ERROR at line 2:
ORA-06550: line 2, column 32:
PLS-00103: Encountered the symbol "AS" when expecting one of the following:
:= . ( % ;
ORA-06550: line 3, column 53:
PLS-00103: Encountered the symbol ";" when expecting one of the following:
, from into bulk


SQL> BEGIN
  2  DMBS_XDB_CONFIG.SETHTTPSPORT(5500);
  3  END;
  4  /
DMBS_XDB_CONFIG.SETHTTPSPORT(5500);
*
ERROR at line 2:
ORA-06550: line 2, column 1:
PLS-00201: identifier 'DMBS_XDB_CONFIG.SETHTTPSPORT' must be declared
ORA-06550: line 2, column 1:
PL/SQL: Statement ignored


SQL> ^XDMBS_XDB_CONFIG.SETHTTPSPORT(5500);
*
ERROR at line 2:
ORA-06550: line 2, column 1:
PLS-00201: identifier 'DMBS_XDB_CONFIG.SETHTTPSPORT' must be declared
ORA-06550: line 2, column 1:
PL/SQL: Statement ignored


SQL> BEGIN
  2  DBMS_XDB_CONFIG.SETHTTPSPORT(5500); -- Set HTTPS port to 5500
  3  END;
  4  /

PL/SQL procedure successfully completed.

SQL>





