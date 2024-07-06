# SnippetBox

## Local MySQL

Set up:

```bash
sudo mysql
```

```sql
-- step 1: create a db name: snippetbox
CREATE DATABASE snippetbox CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
-- step 2: use a newly created db
USE snippetbox;
-- step 3: create a table: snippets
CREATE TABLE
    snippets (
        id INTEGER NOT NULL PRIMARY KEY AUTO_INCREMENT,
        title VARCHAR(100) NOT NULL,
        content TEXT NOT NULL,
        created DATETIME NOT NULL,
        expires DATETIME NOT NULL
    );
-- step 4: index
CREATE INDEX idx_snippets_created ON snippets(created);
-- step 5: insert a first row
INSERT INTO
    snippets (title, content, created, expires)
VALUES
    (
        'An old silent pond',
        'An old silent pond...\nA frog jumps into the pond,\nsplash! Silence again.\n\n– Matsuo Bashō',
        UTC_TIMESTAMP (),
        DATE_ADD (UTC_TIMESTAMP (), INTERVAL 365 DAY)
    );
-- step 6: insert second & third rows
INSERT INTO
    snippets (title, content, created, expires)
VALUES
    (
        'Over the wintry forest',
        'Over the wintry\nforest, winds howl in rage\nwith no leaves to blow.\n\n– Natsume Soseki',
        UTC_TIMESTAMP (),
        DATE_ADD (UTC_TIMESTAMP (), INTERVAL 365 DAY)
    );
INSERT INTO
    snippets (title, content, created, expires)
VALUES
    (
        'First autumn morning',
        'First autumn morning\nthe mirror I stare into\nshows my father''s face.\n\n– Murakami Kijo',
        UTC_TIMESTAMP (),
        DATE_ADD (UTC_TIMESTAMP (), INTERVAL 7 DAY)
    );
-- step 7: create a new user for connecting to MySQL & set its permissions, username = `web`
CREATE USER 'web'@'localhost';
GRANT SELECT, INSERT, UPDATE, DELETE ON snippetbox.* TO 'web'@'localhost';
```

Log in to MySQL with:

- db name = `snippetbox`
- user = `web`

```bash
mysql -D snippetbox -u web
```
