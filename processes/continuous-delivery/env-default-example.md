### Образец .env.default

```
# Название приложения
APP_NAME=ЖивойЖурнал

# URL ftp-сервера
DEPLOY_BASEURL=paste_ftp_server_domain_here

# Основная build-схема приложения
SCHEME=LiveJournal

# Ключи Crashlytics
CRASHLYTICS_API_TOKEN=paste_token_here (https://fabric.io/settings/organizations)
CRASHLYTICS_BUILD_SECRET=paste_secret_here (https://fabric.io/settings/organizations)

# Имя .xcodeproj-файла
XCODEPROJ_NAME=LiveJournal.xcodeproj

# Имя .xcworkspace-файла
XCWORKSPACE_NAME=LiveJournal.xcworkspace

# Путь до Info.plist-файла
INFO_PLIST_PATH='LiveJournal/Info.plist'

# Web-hook URL для Slack
SLACK_URL=paste_slack_webhook_url_here
```
