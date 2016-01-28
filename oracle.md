Anonymous TABLE or VARRAY type in Oracle

http://laurentschneider.com/wordpress/2007/12/predefined-collections.html

http://stackoverflow.com/a/8786450/479159
`Here are some I use quite often (well odcivarchar2list not so much, as it chews up a lot of memory: for strings I prefer dbms_debug_vc2coll).`

```sql
select * from table(sys.ODCIVarchar2List('AAA','BBB','CCC'));

select * from table(sys.dbms_debug_vc2coll('AAA', 'BBB', 'CCC'));

COLUMN_VALUE
------------
AAA
BBB
CCC
```
