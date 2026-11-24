# Postiz – wersja Apturn Social

Fork [gitroomhq/postiz-app](https://github.com/gitroomhq/postiz-app) (AGPL-3.0) używany na
`postiz.apturn.pl`. Gałąź `apturn` = tag upstream + zmiany poniżej.

## Zmiany względem upstream
- Branding: logo i wordmark Apturn (`components/new-layout/logo.tsx`,
  `components/ui/logo-text.component.tsx`), favicony w `apps/frontend/public`,
  „Apturn Social” w tytułach stron, ekran logowania bez marketingu Postiz.
- Link do kodu źródłowego na ekranie logowania (AGPL-3.0 §13).
- Język polski: `locales/pl/translation.json` + `pl` w `i18n.config.ts`
  (utrzymywane w tym forku; PR upstream #2427 zamknięty, wymagał CLA).
- Nazwa „Postiz” w tekstach interfejsu, błędach i mailach zamieniona na „Apturn Social”
  (wszystkie języki w `locales` i teksty domyślne w kodzie; klucze, env, identyfikatory bez zmian).
- Rzeczy upstreamu ukryte warunkiem `billingEnabled` (u nas zawsze fałsz, bo nie ma Stripe):
  linki docs.postiz.com, CLI, konektory z katalogów Claude/ChatGPT, film w onboardingu.
- Celowo zostają: `mcp.relay.service.ts` i `agencies.service.ts` (nieosiągalne u nas), opinie
  klientów Postiza w `testomonials.tsx` (nieużywane; nie wolno ich podpisać naszą nazwą),
  narzędzie MCP `ask_postiz`, User-Agent do WordPressa i Tumblra, schemat `postiz://`.
- Plan przenosin na własną domenę i zrzuty leżą lokalnie w `docs/` (repo jest publiczne, katalog poza gitem).
- Workflow `.github/workflows/apturn-image.yml` buduje `ghcr.io/madern/postiz-app:apturn-<tag>`
  (tagi produkcyjne tylko z gałęzi `apturn`, gałąź `apturn-rebrand` dostaje `:apturn-rebrand`);
  workflowy upstream usunięte z tej gałęzi.

## Aktualizacja do nowej wersji Postiz
1. `git fetch upstream --tags` i `git rebase --onto <nowy-tag> <stary-tag> apturn`.
2. Po konfliktach w `translation.json` uzupełnić nowe klucze w `pl` i ponownie zamienić „Postiz” w tekstach.
   Kontrola: `git grep -nw Postiz -- apps/frontend/src libraries/react-shared-libraries/src/translation`
   ma zwrócić tylko komentarze.
3. Zmienić `UPSTREAM` w workflow, push gałęzi `apturn`, poczekać na build.
4. Na serwerze podmienić tag obrazu w `~/postiz/docker-compose.yml` i `docker compose up -d postiz`.
