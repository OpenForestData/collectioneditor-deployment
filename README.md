# Collection Editor Deployment
This project is responsible for implementing the docker-compose stack of the Collection Editor application.

## Installation
Installing [docker](https://docs.docker.com/) and [docker-compose](https://docs.docker.com/compose/install/) is required to run the application.

Stack uses containers hosted on Whiteaster's docker registry. Images tagged "latest" are the latest stable versions.

Wherever there are placeholders, e.g. `dataverse_access_token_here` or `PasswordHere123`, secure passwords should be generated or docker secret should be used.

### Application environment variables
The service `ce_db` has the following variables:
```
- POSTGRES_USER=ce_user
- POSTGRES_PASSWORD=PasswordHere123
- POSTGRES_DB=collection_editor
```

The service `ce_db` has the following variables:
```
- MONGO_INITDB_DATABASE=collection_editor
- MONGO_INITDB_ROOT_USERNAME=ce_user
- MONGO_INITDB_ROOT_PASSWORD=PasswordHere123
```

The service `ce_backend` has the following variables:
```
- DEBUG=True
- DB_NAME=collection_editor
- DB_HOST=ce_db
- DB_ENGINE=postgres
- DB_DATABASE=collection_editor
- DB_USER=ce_user
- DB_PASSWORD=PasswordHere123
- MONGO_HOST=ce_mongo
- MONGO_DATABASE=collection_editor
- MONGO_USER=ce_user
- MONGO_PASSWORD=PasswordHere123
- LDAP_HOST='ldap://ldap_host_here'
- LDAP_USERNAME='cn=username,ou=ldap,dc=here,dc=local'
- LDAP_PASSWORD='PasswordHere123'
- LDAP_SEARCH_HOST='ou=search,ou=host,dc=here'
- LDAP_FORMAT='sAMAccountName'
- DATAVERSE_URL=https://data-epuszcza.biaman.pl
- DATAVERSE_ACCESS_TOKEN=dataverse_access_token_here
- SECRET_KEY=SECRET_KEY_token_here
```

The service `ce_frontend` has the following variables:
```
- PROD=true
- HOSTNAME=${http}://${URL}/api/
```

## Deployment
```
$ URL="localhost" docker-compose pull
$ URL="localhost" docker-compose up -d
```

The `http` and `URL` variables define the addresses on which the application is to be launched and on which frontend the backend listens.
The `http` variable takes the value: `http` or `https`
The `URL` variable defines the target address of the application, for example `localhost` or `collectioneditor.biaman.pl`.

In the configuration presented above, the application will be launched and will be available at `http://localhost`.

## Contribution
The project was performed by Whiteaster sp.z o.o., with register office in Chorzów, Poland - www.whiteaster.com and provided under the GNU GPL v.3 license to the Contracting Entity - Mammal Research Institute Polish Academy of Science in Białowieża, Poland.We are proud to release this project under an Open Source license. If you want to share your comments, impressions or simply contact us, please write to the following e-mail address: info@whiteaster.com