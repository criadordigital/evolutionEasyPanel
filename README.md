# evolutionEasyPanel
Como instalar a Evolution API no EasyPanel.

Links úteis:
- https://acte.ltd/utils/randomkeygen
- https://hub.docker.com/r/atendai/evolution-api/tags
- https://github.com/EvolutionAPI/evolution-api

## Instalar Postgres e Redis
```
{
  "services": [
    {
      "type": "postgres",
      "data": {
        "projectName": "evo-postgres",
        "serviceName": "evo-postgres",
        "image": "bitnami/postgresql:16"
      }
    },
    {
      "type": "redis",
      "data": {
        "projectName": "evo-redis",
        "serviceName": "evo-redis",
        "password": "senharedis"
      }
    }
  ]
}
```

## Variáveis
```
{
  "services": [
    {
      "type": "app",
      "data": {
        "projectName": "evolution",
        "serviceName": "evolution",
        "source": {
          "type": "image",
          "image": "atendai/evolution-api:v2.2.0"
        },
        "domains": [
          {
            "host": "$(EASYPANEL_DOMAIN)",
            "port": 8080
          }
        ],
        "env":""SERVER_TYPE=http\
SERVER_PORT=8080\
# Server URL - Set your application url\
SERVER_URL=https://$(PRIMARY_DOMAIN)\
SENTRY_DSN=\
# Cors - * for all or set separate by commas -  ex.: \'yourdomain1.com, yourdomain2.com\'\
CORS_ORIGIN=*\
CORS_METHODS=GET,POST,PUT,DELETE\
CORS_CREDENTIALS=true\
# Determine the logs to be displayed\
LOG_LEVEL=ERROR,WARN,DEBUG,INFO,LOG,VERBOSE,DARK,WEBHOOKS,WEBSOCKET\
LOG_COLOR=true\
# Log Baileys - \"fatal\" | \"error\" | \"warn\" | \"info\" | \"debug\" | \"trace\"\
LOG_BAILEYS=error\
# Determine how long the instance should be deleted from memory in case of no connection.\
# Default time: 5 minutes\
# If you don\'t even want an expiration, enter the value false\
DEL_INSTANCE=false\
# Provider: postgresql | mysql\
DATABASE_PROVIDER=postgresql\
DATABASE_CONNECTION_URI=SUA URL POSTGRES\
# Client name for the database connection\
# It is used to separate an API installation from another that uses the same database.\
DATABASE_CONNECTION_CLIENT_NAME=evolution_v2\
# Cache - Environment variables\
# Redis Cache enabled\
CACHE_REDIS_ENABLED=true\
CACHE_REDIS_URI=SUA URL REDIS\
# Prefix serves to differentiate data from one installation to another that are using the same redis\
CACHE_REDIS_PREFIX_KEY=evolution_v2\
# Enabling this variable will save the connection information in Redis and not in the database.\
CACHE_REDIS_SAVE_INSTANCES=false\
# Local Cache enabled\
CACHE_LOCAL_ENABLED=false\
# Define a global apikey to access all instances.\
# OBS: This key must be inserted in the request header to create an instance.\
AUTHENTICATION_API_KEY=SUA CHAVE API\
# If you leave this option as true, the instances will be exposed in the fetch instances endpoint.\
AUTHENTICATION_EXPOSE_IN_FETCH_INSTANCES=true\
LANGUAGE=en\
# Choose the data you want to save in the application\'s database\
DATABASE_SAVE_DATA_INSTANCE=true\
DATABASE_SAVE_DATA_NEW_MESSAGE=true\
DATABASE_SAVE_MESSAGE_UPDATE=true\
DATABASE_SAVE_DATA_CONTACTS=true\
DATABASE_SAVE_DATA_CHATS=true\
DATABASE_SAVE_DATA_LABELS=true\
DATABASE_SAVE_DATA_HISTORIC=true\
# RabbitMQ - Environment variables\
RABBITMQ_ENABLED=false\
RABBITMQ_URI=amqp://localhost\
RABBITMQ_EXCHANGE_NAME=evolution\
# Global events - By enabling this variable, events from all instances are sent in the same event queue.\
RABBITMQ_GLOBAL_ENABLED=false\
# Choose the events you want to send to RabbitMQ\
RABBITMQ_EVENTS_APPLICATION_STARTUP=false\
RABBITMQ_EVENTS_INSTANCE_CREATE=false\
RABBITMQ_EVENTS_INSTANCE_DELETE=false\
RABBITMQ_EVENTS_QRCODE_UPDATED=false\
RABBITMQ_EVENTS_MESSAGES_SET=false\
RABBITMQ_EVENTS_MESSAGES_UPSERT=false\
RABBITMQ_EVENTS_MESSAGES_EDITED=false\
RABBITMQ_EVENTS_MESSAGES_UPDATE=false\
RABBITMQ_EVENTS_MESSAGES_DELETE=false\
RABBITMQ_EVENTS_SEND_MESSAGE=false\
RABBITMQ_EVENTS_CONTACTS_SET=false\
RABBITMQ_EVENTS_CONTACTS_UPSERT=false\
RABBITMQ_EVENTS_CONTACTS_UPDATE=false\
RABBITMQ_EVENTS_PRESENCE_UPDATE=false\
RABBITMQ_EVENTS_CHATS_SET=false\
RABBITMQ_EVENTS_CHATS_UPSERT=false\
RABBITMQ_EVENTS_CHATS_UPDATE=false\
RABBITMQ_EVENTS_CHATS_DELETE=false\
RABBITMQ_EVENTS_GROUPS_UPSERT=false\
RABBITMQ_EVENTS_GROUP_UPDATE=false\
RABBITMQ_EVENTS_GROUP_PARTICIPANTS_UPDATE=false\
RABBITMQ_EVENTS_CONNECTION_UPDATE=false\
RABBITMQ_EVENTS_REMOVE_INSTANCE=false\
RABBITMQ_EVENTS_LOGOUT_INSTANCE=false\
RABBITMQ_EVENTS_CALL=false\
RABBITMQ_EVENTS_TYPEBOT_START=false\
RABBITMQ_EVENTS_TYPEBOT_CHANGE_STATUS=false\
# SQS - Environment variables\
SQS_ENABLED=false\
SQS_ACCESS_KEY_ID=\
SQS_SECRET_ACCESS_KEY=\
SQS_ACCOUNT_ID=\
SQS_REGION=\
# Websocket - Environment variables\
WEBSOCKET_ENABLED=false\
WEBSOCKET_GLOBAL_EVENTS=false\
# WhatsApp Business API - Environment variables\
# Token used to validate the webhook on the Facebook APP\
WA_BUSINESS_TOKEN_WEBHOOK=evolution\
WA_BUSINESS_URL=https://graph.facebook.com\
WA_BUSINESS_VERSION=v20.0\
WA_BUSINESS_LANGUAGE=en_US\
# Global Webhook Settings\
# Each instance\'s Webhook URL and events will be requested at the time it is created\
WEBHOOK_GLOBAL_ENABLED=false\
# Define a global webhook that will listen for enabled events from all instances\
WEBHOOK_GLOBAL_URL=\'\'\
# With this option activated, you work with a url per webhook event, respecting the global url and the name of each event\
WEBHOOK_GLOBAL_WEBHOOK_BY_EVENTS=false\
# Set the events you want to hear\
WEBHOOK_EVENTS_APPLICATION_STARTUP=false\
WEBHOOK_EVENTS_QRCODE_UPDATED=true\
WEBHOOK_EVENTS_MESSAGES_SET=true\
WEBHOOK_EVENTS_MESSAGES_UPSERT=true\
WEBHOOK_EVENTS_MESSAGES_EDITED=true\
WEBHOOK_EVENTS_MESSAGES_UPDATE=true\
WEBHOOK_EVENTS_MESSAGES_DELETE=true\
WEBHOOK_EVENTS_SEND_MESSAGE=true\
WEBHOOK_EVENTS_CONTACTS_SET=true\
WEBHOOK_EVENTS_CONTACTS_UPSERT=true\
WEBHOOK_EVENTS_CONTACTS_UPDATE=true\
WEBHOOK_EVENTS_PRESENCE_UPDATE=true\
WEBHOOK_EVENTS_CHATS_SET=true\
WEBHOOK_EVENTS_CHATS_UPSERT=true\
WEBHOOK_EVENTS_CHATS_UPDATE=true\
WEBHOOK_EVENTS_CHATS_DELETE=true\
WEBHOOK_EVENTS_GROUPS_UPSERT=true\
WEBHOOK_EVENTS_GROUPS_UPDATE=true\
WEBHOOK_EVENTS_GROUP_PARTICIPANTS_UPDATE=true\
WEBHOOK_EVENTS_CONNECTION_UPDATE=true\
WEBHOOK_EVENTS_REMOVE_INSTANCE=false\
WEBHOOK_EVENTS_LOGOUT_INSTANCE=false\
WEBHOOK_EVENTS_LABELS_EDIT=true\
WEBHOOK_EVENTS_LABELS_ASSOCIATION=true\
WEBHOOK_EVENTS_CALL=true\
# This events is used with Typebot\
WEBHOOK_EVENTS_TYPEBOT_START=false\
WEBHOOK_EVENTS_TYPEBOT_CHANGE_STATUS=false\
# This event is used to send errors\
WEBHOOK_EVENTS_ERRORS=false\
WEBHOOK_EVENTS_ERRORS_WEBHOOK=\
# Name that will be displayed on smartphone connection\
CONFIG_SESSION_PHONE_CLIENT=Evolution API\
# Browser Name = Chrome | Firefox | Edge | Opera | Safari\
CONFIG_SESSION_PHONE_NAME=Chrome\
# Whatsapp Web version for baileys channel\
# https://web.whatsapp.com/check-update?version=0&platform=web\
CONFIG_SESSION_PHONE_VERSION=2.3000.1015901307\
# Set qrcode display limit\
QRCODE_LIMIT=30\
# Color of the QRCode on base64\
QRCODE_COLOR=\'#175197\'\
# Typebot - Environment variables\
TYPEBOT_ENABLED=false\
# old | latest\
TYPEBOT_API_VERSION=latest\
# Chatwoot - Environment variables\
CHATWOOT_ENABLED=false\
# If you leave this option as false, when deleting the message for everyone on WhatsApp, it will not be deleted on Chatwoot.\
CHATWOOT_MESSAGE_READ=true\
# If you leave this option as true, when sending a message in Chatwoot, the client\'s last message will be marked as read on WhatsApp.\
CHATWOOT_MESSAGE_DELETE=true\
# If you leave this option as true, a contact will be created on Chatwoot to provide the QR Code and update messages about the instance.\
CHATWOOT_BOT_CONTACT=true\
# This db connection is used to import messages from whatsapp to chatwoot database\
CHATWOOT_IMPORT_DATABASE_CONNECTION_URI=postgresql://user:passwprd@host:5432/chatwoot?sslmode=disable\
CHATWOOT_IMPORT_PLACEHOLDER_MEDIA_MESSAGE=true\
# OpenAI - Environment variables\
OPENAI_ENABLED=false\
# Dify - Environment variables\
DIFY_ENABLED=false\
# Amazon S3 - Environment variables\
S3_ENABLED=false\
S3_ACCESS_KEY=\
S3_SECRET_KEY=\
S3_BUCKET=evolution\
S3_PORT=443\
S3_ENDPOINT=s3.domain.com\
S3_REGION=eu-west-3\
S3_USE_SSL=true\
# AMAZON S3 - Environment variables\
# S3_ENABLED=true\
# S3_BUCKET=bucket_name\
# S3_ACCESS_KEY=access_key_id\
# S3_SECRET_KEY=secret_access_key\
# S3_ENDPOINT=s3.amazonaws.com # region: s3.eu-west-3.amazonaws.com\
# S3_REGION=eu-west-3\
# MINIO Use SSL - Environment variables\
# S3_ENABLED=true\
# S3_ACCESS_KEY=access_key_id\
# S3_SECRET_KEY=secret_access_key\
# S3_BUCKET=bucket_name\
# S3_PORT=443\
# S3_ENDPOINT=s3.domain.com\
# S3_USE_SSL=true\
# S3_REGION=eu-south",
        "mounts": [
          {
            "type": "volume",
            "name": "evolution_instances",
            "mountPath": "/evolution/instances"
          }
        ]
      }
    }
  ]
}
```

