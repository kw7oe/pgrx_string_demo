## A example of PostgreSQL extensions using `pgrx`

This project includes a simple PostgreSQL extension written in
Rust, using the [`pgrx` crate][0]. This extension contains the following
string manipulations functions:

- `to_title`: Convert a given string to title case.
- `emojify`: Convert any emoji shortcode in a string to emoji.

This is extension is for demonstration and learning purposes and by no mean for
using it in production.

If you would like to learn more about it you can refer to this post:
[Writing PostgreSQL extension in Rust With `pgrx`](https://kaiwern.com/posts/2022/07/20/writing-postgresql-extension-in-rust-with-pgx/)

## Getting Started

1. Install and setup `cargo-pgrx`. For more, refer to the [Getting Started][1] of
   `pgrx`

```
cargo install cargo-pgrx
cargo pgrx init
```

2. Clone this repository and change directory into it.
3. Run it using `cargo pgrx run pg15`. This will spin up a PostgreSQL.
4. In your `psql` session, load the extension first:

```sql
hello_world=#  create extension hello_world;
CREATE EXTENSION
hello_world=# \df
                             List of functions
 Schema |       Name        | Result data type | Argument data types | Type
--------+-------------------+------------------+---------------------+------
 public | emojify           | text             | string text         | func
 public | hello_hello_world | text             |                     | func
 public | to_title          | text             | string text         | func
(3 rows)
```

5. Now with everything loaded you can run the following SQL:

```sql
hello_world=# select hello_hello_world();
 hello_hello_world
--------------------
 Hello, hello_world
(1 row)

hello_world=# select to_title('this is so cool');
    to_title
-----------------
 This Is So Cool
(1 row)

hello_world=# select emojify('I love pgrx :100:');
    emojify
----------------
 I love pgrx 💯
(1 row)
```

[0]: https://github.com/pgcentralfoundation/pgrx
[1]: https://github.com/pgcentralfoundation/pgrx?tab=readme-ov-file#getting-started
