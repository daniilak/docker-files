version: '3'
x-common-variables: &common-variables
    POSTGRES_USER : user_name
    POSTGRES_PASSWORD : pass
    POSTGRES_DB : database_name
services:
    postgres:
        image: postgres
        volumes:
        - 'postgres:/var/lib/postgresql/data'
        networks:
            - default
        environment:
            <<: *common-variables
            PGDATA : /var/lib/postgresql/data/pgdata
        labels:
            description: "Postgresql Database"
            service: "postgresql"
    api_flask:
        image: image_api_flask
        environment:
            <<: *common-variables
            POSTGRES_HOST : 192.168.0.202
        build: .
        ports:
            - 5087:5087
        privileged: true
        depends_on:
            - 'postgres'
        command: >
            python3 app/app.py
    api_demon:
        image: image_api_flask
        depends_on:
            - 'postgres'
        command: >
            python3 app/demon.py
volumes:
    postgres:

