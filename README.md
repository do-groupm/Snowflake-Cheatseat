# Snowflake-Cheatseat
Snowflake's most frequently needed commands gathered in one place

### What's my current user, role, warehouse, database, etc?
```
SELECT CURRENT_USER();
SELECT CURRENT_ROLE();
SELECT CURRENT_WAREHOUSE();
SELECT CURRENT_DATABASE();
```
### How do I create a new database user?
```
SHOW ROLES;
USE ROLE ACCOUNTADMIN;
-- USE ROLE SECURITYADMIN;
CREATE USER {username} PASSWORD = '{password}' MUST_CHANGE_PASSWORD = TRUE;
-- Grant usage on a database and warehouse to a role
SHOW GRANTS TO ROLE {role};
GRANT USAGE ON WAREHOUSE {warehouse} TO ROLE {role};
GRANT USAGE ON DATABASE {database} TO ROLE {role};
```
