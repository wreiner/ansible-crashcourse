### YAML?

- short for "YAML Ain't Markup Language"
- YAML uses indentation
- represent data structures
  - variables
  - lists
  - dictionaries
  - nested objects

    ```
    ---
    # lines starting with # are comments

    app_name: myapp
    port: 8080
    debug: true

    # Define a list of users
    users:
      - name: Alice
        email: alice@example.com
      - name: Bob
        email: bob@example.com
      - name: Charlie
        email: charlie@example.com

    # Define a dictionary of database settings
    database:
      host: localhost
      port: 5432
      name: mydb
      user: dbuser
      password: dbpass
    ```