- [PostgreSQL](#postgresql)
  * [好處](#--)
  * [How to use](#how-to-use)
  * [CREATE database](#create-database)
  * [Start prisma default](#start-prisma-default)
  * [Show database](#show-database)
  * [Show current table view](#show-current-table-view)
  * [Show type enum table](#show-type-enum-table)
  * [Connect database](#connect-database)
  * [show data from the table](#show-data-from-the-table)
  * [逆向生成数据模型](#--------)
  * [Postgres會幫你做database](#postgres----database)
  * [Prisma 模型生成 table](#prisma------table)
  * [生成model裡的資料 放進prisma package裡](#--model-------prisma-package-)
  * [Prisma studio](#prisma-studio)
  * [Postgres version](#postgres-version)


    # PostgreSQL

    Tags: Mysql, PostgreSQL, Prisma

    ## 好處

    如果你用 mysql 那樣你要寫 mysql的結構，如果你用 mongoose 那樣你就要寫mongoose的結構

    而prisma 它能work with 這些database 而不需要 更改 寫的結構

    為什麼能那麼做到呢，因為 prisma grab 我們的database 轉換去 GraphQL API，所以 我們的 server backend 怎樣都能明白了

    Flow

    1. Client to Server 不是通過 REST APIs了 而是 GraphQL 
    2. 然後 server backend 去 database 而是通過 Prisma 但是 Prisma(也就是 GraphQL)

    ## How to use

    1. Open postgreSQL
    2. Open Terminal
    3. psql (enter into postgreSQL environment)
    4. create new database for your project
    5. connect the database (terminal #=\c (database_name;)
    6. example of command to create type and table for postgreSQL

    ```bash
    -- Create a custom type
    CREATE TYPE "user_role_enum" AS ENUM ('user', 'admin', 'superadmin');

    -- Create a table
    CREATE TABLE "users"(
        "id" BIGSERIAL PRIMARY KEY NOT NULL,
        "name" VARCHAR(255) NOT NULL,
        "email" VARCHAR(255) UNIQUE NOT NULL,
        "role" user_role_enum NOT NULL DEFAULT('user')
    );

    -- Create a table
    CREATE TABLE "posts"(
        "id" BIGSERIAL PRIMARY KEY NOT NULL,
        "title" VARCHAR(255) NOT NULL,
        "body" TEXT,
        "userId" INTEGER NOT NULL,
        FOREIGN KEY ("userId") REFERENCES "users"("id")
    );

    -- Create data
    INSERT INTO "users" ("name", "email", "role")
    VALUES('John Doe', 'john@email.com', 'admin'),
    ('jane Doe', 'jane@email.com', 'admin'),
    ('Ahmed Hadjou', 'ahmed@hadjou.com', 'user');

    INSERT INTO "posts" ("title", "body", "userId")
    VALUES('Hello World!!', 'Hey guys, I see a rainbow through this prisma :D', 1),
    ('So do I', 'It looks cooool!!!', 2),
    ('It does', 'Yeahhh', 1);
    ```

    DROP table and type

    ```bash
    -- Drop schema
    DROP TABLE "User"; DROP TABLE "Post"; DROP TYPE "user_role_enum";
    ```

    ## CREATE database

    ```bash
    CREATE DATABSE database_name;
    ```

    在 postgresSQL裡 一個 database的icon 就代表那個 database

    ## Start prisma default

    ```bash
    npm install @prisma/client 
    npx prisma init
    ```

    ## Show database

    ```bash
    #=\l
    ```

    ## Show current table view

    ```bash
    #=\d
    ```

    ## Show type enum table

    ```bash
    #=\dT+
    ```

    ## Connect database

    ```bash
    #=\c database_name
    ```

    ## show data from the table

    ```sql
    Select * from users;
    ```

    ## 逆向生成数据模型

    需要 create 好table sql 先

    ```bash
    $ npx prisma introspects
    ```

    ## Postgres會幫你做database

    不需要去 postgres裡 做database， 你run `migrate` 它會幫你生成了

    ## Prisma 模型生成 table

    需要在schema.prisma 寫好model

    migrate後 就能 進去 studio + 你的 data了 

    ```bash
    npx prisma migrate dev --name "Add Card Model"
    ```

    or

    ```bash
    npx prisma migrate dev --preview-feature

    migrate name: Add Card Model
    ```

    ## 生成model裡的資料 放進prisma package裡

    ```sql
    npx prisma generate
    ```

    ## Prisma studio

    ```bash
    $ npx prisma studio
    ```

    ## Postgres version

    ```bash
    postgres -V
    psql -V
    ```
