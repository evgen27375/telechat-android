# TELECHAT for Android

TELECHAT — мессенджер на базе открытого клиента **Telegram for Android**
(<https://github.com/DrKLO/Telegram>) со встроенным MTProto-прокси, позволяющим
пользоваться Telegram без отдельного VPN.

## Лицензия

Проект распространяется по **GNU General Public License v2** (как и оригинальный
Telegram for Android). Полный текст — в файле [`LICENSE`](LICENSE).

Это форк. Оригинальный код: © Telegram Messenger LLP и участники проекта Telegram.
Изменения TELECHAT добавлены поверх и также лицензируются под GPLv2.

## Основные отличия от оригинала

- Название и брендинг — TELECHAT.
- Пакет приложения — `ru.kapitanqr.telechat`.
- Встроенный MTProto Fake-TLS прокси, включаемый автоматически.
- Логика включения прокси: `SharedConfig.ensureTelechatProxy()`, вызывается из
  `ApplicationLoader` при старте.

## Сборка

См. [`docs/BUILD.md`](../docs/BUILD.md) (вне репозитория, в рабочей директории проекта)
или кратко:

```bash
# JDK 17, Android SDK 36, NDK 27.2.12479018, cmake 3.22.1
./gradlew :TMessagesProj_AppStandalone:assembleAfatStandalone
```

## Секреты (не в репозитории)

Следующее НЕ хранится в git и подставляется при сборке из `local.properties`:

- `TELECHAT_PROXY_SERVER` / `TELECHAT_PROXY_PORT` / `TELECHAT_PROXY_SECRET` — адрес прокси;
- `TELECHAT_APP_ID` / `TELECHAT_APP_HASH` — ключи Telegram API (my.telegram.org);
- `TMessagesProj/config/release.keystore` — ключ подписи.

Пример `local.properties`:

```properties
sdk.dir=/path/to/android-sdk
TELECHAT_PROXY_SERVER=your.proxy.host
TELECHAT_PROXY_PORT=443
TELECHAT_PROXY_SECRET=ee...
TELECHAT_APP_ID=1234567
TELECHAT_APP_HASH=your_api_hash
```

При сборке без этих значений приложение компилируется, но встроенный прокси не активируется,
а для логина используются тестовые ключи Telegram.
