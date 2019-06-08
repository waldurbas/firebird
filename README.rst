======================================
firebirdsql (Go firebird sql driver)
======================================

Firebird RDBMS http://firebirdsql.org SQL driver for Go

.. image:: https://travis-ci.org/nakagami/firebirdsql.svg?branch=master
    :target: https://travis-ci.org/nakagami/firebirdsql

Requirements
-------------

* Firebird 2.58 or higher
* Golang 1.12 or higher

Installation
-------------

::

   $ go get github.com/cznic/mathutil
   $ go get github.com/kardianos/osext
   $ go get github.com/shopspring/decimal
   $ go get github.com/waldurbas/firebirdsql
   $ go get gitlab.com/nyarla/go-crypt
   $ go get github.com/jmoiron/sqlx


Example
-------------

::

   package main

   import (
       "fmt"

       _ "github.com/waldurbas/firebirdsql"
  	   "github.com/jmoiron/sqlx"
   )

   func main() {
       var n int
       db, err := sqlx.Connect("firebirdsql", "user:password@server/3051:db.fdb")
   	   if err != nil {
            panic(err.Error())
       }

       defer db.Close()
       db.QueryRow("select count(*) from rdb$relations").Scan(&n)
       fmt.Println("Relations.Count=", n)
   }


Connection string
--------------------------

   user:pass@server/port_number:dbalias


General
=========

- user: login user
- pass: login password
- server: Firebird server's host name or IP address.
- portNumber: Port number. default value is 3051.
- dbalias: alias name).


Optional
=========

param1, param2... are

.. csv-table::
   :header: Name,Description,Default,Note

   auth_plugin_name,Authentication plugin name.,Srp,Srp256/Srp/Legacy_Auth are available.
   column_name_to_lower,Force column name to lower,false,For "github.com/jmoiron/sqlx"
   role,Role name,
   tzname, Time Zone name, For Firebird 4.0+
   wire_crypt,Enable wire data encryption or not.,true,For Firebird 3.0+

