# 05: i18n lockstep and settings search

**What to build:** Every new string exists in all 15 locale catalogs with the same keys as `en`. Account recent-session import is registered in settings search so "import" / "recent sessions" finds it.

**Blocked by:** 02, 03

**Status:** done (commit d696313c)

- [x] `en` keys exist for import hint, import listed, partial failure, sidebar CTA
- [x] de es fil fr id it ja ko pt-BR ru ta uk zh zh-TW match those keys
- [x] settingsCatalog account.callLogs entry covers the new controls
