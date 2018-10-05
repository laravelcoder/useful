MySQL is an open source relational database managed system (RDBMS) that enables users and applications to store, organize, and retrieve their data. It has an access control system that consists of permissions that the users can have within tables and databases. In this tutorial, we will explain how to create a new user in MySQL, and grant permissions to that use. Creating a new user in MySQL database and granting permissions is an easy task if you follow this tutorial carefully.


Step 1:  Log in to MySQL
To log in to our MySQL system we use the following command:

# mysql -u root -p
By executing this command we tell the MySQL client to log us in with the root user and to prompt us for the user’s password.

If you haven’t installed MySQL on your server, you can check our tutorial on how to install MySQL on Ubuntu 16.04.

Step 2: Create MySQL User
Create a new MySQL user with the following query:

CREATE USER 'new_user'@'localhost' IDENTIFIED BY 'password';
Pro-tip: always use a strong password for all your accounts. You can generate one from the command line.

Another interesting thing to note about this command is that the hostname of the new user we just created can be a different hostname or IP address if we want the user to log in remotely.
As an example:

CREATE USER 'new_user'@'10.20.30.111' IDENTIFIED BY 'password';
Let’s say we want to provide our new user with permissions so that they can read data from all databases on our MySQL server. We do that by typing in the following command:

GRANT SELECT ON *.* TO 'new_user'@'localhost';
By executing the query above we instruct MySQL to give our new user permission to use the command SELECT to read from databases on our MySQL server, we used the SELECT keyword in order to do that. GRANT SELECT tells MySQL that the user will have nothing other than permissions to read data from a given database or databases. Granting permissions is typically done in this format:

GRANT <permission type> ON <database>.<table> TO '<username>'@'<host>';
We can also instruct MySQL to take away a certain permission from a user in the same format as above by only replacing the keyword GRANT with REVOKE and the keyword TO with FROM:

REVOKE <permission type> ON <database>.<table> FROM '<username>'@'<host>';
Note: The asterisks that we use for the database and table positions in the query above are wildcards and match any database or table depending on position.
In order for our new set permissions to take effect we need to reload all the privileges:

FLUSH PRIVILEGES;
Step 3: Granting users other types of permissions in MySQL
In the section above we saw how to grant read permissions to the user by using the keyword SELECT. In this section, we will explore other keywords that will allow us to set various types of permissions on the user.

USAGE – gives the user permission to log in to the MySQL server(given by default when creating a new user)
SELECT – gives the user permission to use the select command to fetch data from tables
INSERT – gives the user permission to add new rows into tables
UPDATE – gives the user permission to modify the existing rows in tables
DELETE – gives the user permission to delete existing rows from tables
CREATE – gives the user permission to create new tables or databases
DROP – gives the user permission to remove existing tables or databases
ALL PRIVILEGES – gives the user permission to have unrestricted access on a database or the whole system(by using an asterisk in the database position)
GRANT OPTION – gives the user permission to grant or remove other users’ permissions
Step 4: Delete user in MySQL
Deleting users is done the same way as it is with databases or tables by using the DROP command:

DROP USER 'new_user'@'localhost';
Step 5: Test user in MySQL
Finally, we can test our new user, type in the following command to end the currently active session:

exit;
And then we log back in by typing in this command in the shell prompt:

mysql -u new_user -p
Note: Remember to substitute new_user for your own desired username.

That’s it, now you have created a new MySQL user and assigned permissions to it.
