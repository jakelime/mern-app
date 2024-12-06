# Helper on setting up MongoDB

On your host machine

```shell
# https://linuxize.com/post/how-to-install-mongodb-on-debian-10
sudo apt install dirmngr gnupg apt-transport-https software-properties-common ca-certificates curl -y
curl -fsSL https://www.mongodb.org/static/pgp/server-4.2.asc | sudo apt-key add -
sudo add-apt-repository 'deb https://repo.mongodb.org/apt/debian buster/mongodb-org/4.2 main'
sudo apt install mongodb-org

# evaluate connection
mongo --eval 'db.runCommand({ connectionStatus: 1 })'
```


```shell
sudo apt-get install gnupg curl
curl -fsSL https://www.mongodb.org/static/pgp/server-8.0.asc | \
   sudo gpg -o /usr/share/keyrings/mongodb-server-8.0.gpg \
   --dearmor
echo "deb [ signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg ] http://repo.mongodb.org/apt/debian bookworm/mongodb-org/8.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-8.0.list
sudo apt-get update
sudo apt-get install -y mongodb-org=8.0.0 mongodb-org-database=8.0.0 mongodb-org-server=8.0.0 mongodb-mongosh mongodb-org-mongos=8.0.0 mongodb-org-tools=8.0.0
```


## Uninstall MongoDB

```shell
sudo service mongod stop
sudo apt-get purge mongodb-org*
sudo rm -r /var/log/mongodb /var/lib/mongodb
service mongod status
```


## Example


```shell

➜  my-react-app git:(main) mongosh mongodb://localhost:27017 --username arunmongo

Enter password: *********

Current Mongosh Log ID: 675266fb9318392efbe94969
Connecting to:          mongodb://<credentials>@localhost:27017/?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+2.3.4
Using MongoDB:          8.0.3
Using Mongosh:          2.3.4

For mongosh info see: https://www.mongodb.com/docs/mongodb-shell/

------
   The server generated these startup warnings when booting
   2024-12-06T02:51:37.772+00:00: Using the XFS filesystem is strongly recommended with the WiredTiger storage engine. See http://dochub.mongodb.org/core/prodnotes-filesystem
   2024-12-06T02:51:39.036+00:00: For customers running the current memory allocator, we suggest changing the contents of the following sysfsFile
   2024-12-06T02:51:39.036+00:00: We suggest setting the contents of sysfsFile to 0.
   2024-12-06T02:51:39.036+00:00: Your system has glibc support for rseq built in, which is not yet supported by tcmalloc-google and has critical performance implications. Please set the environment variable GLIBC_TUNABLES=glibc.pthread.rseq=0
   2024-12-06T02:51:39.036+00:00: vm.max_map_count is too low
   2024-12-06T02:51:39.037+00:00: We suggest setting swappiness to 0 or 1, as swapping can cause performance problems.
------

# see all the databases in the cluster that you have access to 
# using the show command
test> show dbs
admin   100.00 KiB
config   12.00 KiB
local    72.00 KiB

# here is no “create” command in the MongoDB Shell. 
# In order to create a database, you will first need to switch the 
# context to a non-existing database using the use command:
test> use my-database
switched to db my-database
my-database> db.user.insert({name: "Ada Lovelace", age: 205})
DeprecationWarning: Collection.insert() is deprecated. Use insertOne, insertMany, or bulkWrite.
{
  acknowledged: true,
  insertedIds: { '0': ObjectId('675267979318392efbe9496a') }
}


# Now your database is created
my-database> show dbs
admin        100.00 KiB
config        12.00 KiB
local         72.00 KiB
my-database   40.00 KiB
```