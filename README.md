<h2>Oracle script for oracle11g</h2>
  <p>DB connection; schema, table, table space creation; fix insufficient privileges</p>

<h3>Connect DB using cmd SQL-PLUS</h3>
  <p>(open commad promt)</p>
  <pre>
    <code>
      sqlplus / as sysdba
      username: connect / as sysdba
      pass: oracle11g
    </code>
  </pre>
  <p>OR (open sql-plus)</p>
  <pre>
    <code>
      connect / as sysdba
      pass: oracle11g
    </code>
  </pre>
  
  <h3>If error occurred: [ora-01031] insufficient privileges</h3>
  solution: 
  <ul>
		<li>start menu-></li>
      <ul>
        <li>Oracle-OraDb11g_Home1-></li>
          <ul>
		        <li>Administration Assistant for windows->-></li>
              <ul>
                <li>Oracle Managed Objects-></li>
                  <ul>
		                <li>DESKTOP-EDIVCBS-></li>
                      <ul>
                        <li>OS Database Administrators-Computer-> 
                          <ul>
                            <li>right click(Add/Remove..) </li>
                            <li>select domain</li>
                            <li>salekin [pc user name]</li>
                            <li>click 'Add'. Then 'Ok'. That's it.</li>
                          </ul>
                        </li>
                      </ul>
                  </ul>
              </ul>
          </ul>
      </ul>
  </ul>
      
  <h3>Displaying username, account_status</h3>
  <pre>
    <code>
      SELECT username, account_status FROM dba_users;
    </code>
  </pre>
  
  <h3>Create table space</h3>
  <pre>
    <code>
      CREATE TABLESPACE "A_SYSTEM_TBS" DATAFILE
      'C:/app/username/oradata/orcl/A_SXSTEM_TBS.dbf'
      SIZE 100M AUTOEXTEND ON NEXT 100M MAXSIZE 8G
      LOGGING
      ONLINE
      PERMANENT
      EXTENT MANAGEMENT LOCAL AUTOALLOCATE
      BLOCKSIZE 8K
      SEGMENT SPACE MANAGEMENT AUTO
      FLASHBACK ON;
    </code>
  </pre>
  
  <pre>
    <code>
      CREATE TABLESPACE "A_INDEX_TBS" DATAFILE
      'C:/app/username/oradata/orcl/A_INDEX_TBS.dbf'
      SIZE 100M AUTOEXTEND ON NEXT 100M MAXSIZE 8G
      LOGGING
      ONLINE
      PERMANENT
      EXTENT MANAGEMENT LOCAL AUTOALLOCATE
      BLOCKSIZE 8K
      SEGMENT SPACE MANAGEMENT AUTO
      FLASHBACK ON;
    </code>
  </pre>
  
  <h3>Drop table space</h3>
  <pre>
    <code>
      DROP TABLESPACE MTK_SYSTEM_TBS
      INCLUDING CONTENTS
      CASCADE CONSTRAINTS;
      OR
      Drop tablespace MTK_SYSTEM_TBS including contents and datafiles; [It'll also delete the allocated physical file]
    </code>
  </pre>
  
  <h3>Create Schema</h3>
  <pre>
    <code>
      CREATE USER A
      IDENTIFIED BY password
      DEFAULT TABLESPACE A_SYSTEM_TBS
      TEMPORARY TABLESPACE TEMP
      PROFILE DEFAULT
      ACCOUNT UNLOCK;
    </code>
  </pre>
  
  <h3>Drop Schema</h3>
  <pre>
    <code>
      DROP USER mtaka CASCADE;
    </code>
  </pre>
  
  <h3>Show all schemas in DB</h3>
  <pre>
    <code>
      select username from dba_users;
      OR
      select * from all_users;
    </code>
  </pre>
  
  <h3>Switching to different Schema</h3>
  <pre>
    <code>
      ALTER SESSION SET CURRENT_SCHEMA = mtaka;
    </code>
  </pre>
  
  <h3>Give all privileges to a user</h3>
  <pre>
    <code>
      grant all privileges to mtaka identified by mtaka;
    </code>
  </pre>
  
