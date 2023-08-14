
## Introduction

MongoDB is a powerful NoSQL document-oriented database, commonly used in modern web development and other applications to store and manage data. This cheat-sheet will cover fundamental MongoDB commands and concepts to help you get started.

## Installation

To use MongoDB, you first need to install it on your system. You can follow these steps to install it on various operating systems:

### Windows

1. Download the MongoDB installer from the official website.
2. Run the installer and follow the on-screen instructions to complete the installation.

### macOS

1. Install MongoDB using Homebrew package manager by running the following command in Terminal:

```bash
brew tap mongodb/brew brew install mongodb-community
```


### Linux

1. On Debian/Ubuntu-based systems, use the package manager:

```bash
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4 echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu $(lsb_release -cs)/mongodb-org/5.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list sudo apt-get update sudo apt-get install -y mongodb-org
```


2. On Red Hat/CentOS-based systems, use:

```bash
sudo vi /etc/yum.repos.d/mongodb-org-5.0.repo
```


Add the following content:

```
[mongodb-org-5.0] name=MongoDB Repository baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/5.0/x86_64/ gpgcheck=1 enabled=1 gpgkey=https://www.mongodb.org/static/pgp/server-5.0.asc
```

Then, install MongoDB:

```bash
sudo yum install -y mongodb-org
```


## Starting MongoDB Service

### Windows

1. Start MongoDB as a service by running the following command in Command Prompt:

```bash
mongod --install
```

2. To start the MongoDB service, use:

```bash
net start MongoDB
```


### macOS and Linux

1. Start MongoDB using the following command:

```bash
sudo systemctl start mongod
```

## Access MongoDB Shell

1. Open a new terminal or command prompt.
2. Use the `mongo` command to access the MongoDB shell:

```bash
mongo
```

## Basic MongoDB Commands

### Show Databases

```js
show dbs
```

### Connect to Database

1. Store a api key to connect to the database

### Create or Switch Database

```js
use your_database_name
```

### Create a Collection


```js
db.createCollection("your_collection_name")
```


### Insert Document

```js
db.your_collection_name.insertOne({ key1: "value1", key2: "value2" })
```

### Find Documents


```js
db.your_collection_name.find()
```

### Find Documents with Criteria

```js
db.your_collection_name.find({ key: "value" })
```

### Update Document

```js
db.your_collection_name.updateOne({ key: "value" }, { $set: { new_key: "new_value" } })
```

### Update Multiple Documents

```js
db.your_collection_name.updateMany({ key: "value" }, { $set: { new_key: "new_value" } })
```

### Delete Document

```js
db.your_collection_name.deleteOne({ key: "value" })
```

### Delete Multiple Documents

```js
db.your_collection_name.deleteMany({ key: "value" })
```

## Conclusion

This cheat-sheet covers the basic usage of MongoDB, including installation, starting the service, accessing the MongoDB shell, and fundamental CRUD operations. It provides a solid foundation to begin working with MongoDB for various projects.

Remember that MongoDB offers many advanced features and capabilities beyond what's covered here. For further exploration, refer to the official [MongoDB documentation](https://www.mongodb.com/docs/). Happy data managing with MongoDB!