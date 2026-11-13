# Postiz – wersja Apturn Social

Fork [gitroomhq/postiz-app](https://github.com/gitroomhq/postiz-app) (AGPL-3.0) używany na
`postiz.apturn.pl`. Gałąź `apturn` = tag upstream + zmiany poniżej.

## Zmiany względem upstream
- Branding: logo i wordmark Apturn (`components/new-layout/logo.tsx`,
  `components/ui/logo-text.component.tsx`), favicony w `apps/frontend/public`,
  „Apturn Social” w tytułach stron, ekran logowania bez marketingu Postiz.
- Link do kodu źródłowego na ekranie logowania (AGPL-3.0 §13).
- Język polski: `locales/pl/translation.json` + `pl` w `i18n.config.ts`
  (zgłoszone do upstream osobnym PR).
- Nazwa „Postiz” w tekstach interfejsu (en, pl) zamieniona na „Apturn Social”.
- Workflow `.github/workflows/apturn-image.yml` buduje `ghcr.io/madern/postiz-app:apturn-<tag>`;
  workflowy upstream usunięte z tej gałęzi.

## Aktualizacja do nowej wersji Postiz
1. `git fetch upstream --tags` i `git rebase --onto <nowy-tag> <stary-tag> apturn`.
2. Po konfliktach w `translation.json` uzupełnić nowe klucze w `pl` i ponownie zamienić „Postiz” w tekstach.
3. Zmienić `UPSTREAM` w workflow, push gałęzi `apturn`, poczekać na build.
4. Na serwerze podmienić tag obrazu w `~/postiz/docker-compose.yml` i `docker compose up -d postiz`.
