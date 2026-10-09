# AGENTS.md — proxmox-perfect-wordpress

Gemeinsame Instruktionsdatei für alle Agenten (Claude, Codex, Gemini); `CLAUDE.md` ist ein
Symlink hierauf. Globale Regeln: `~/Developer/KI/neo.md`.

**Öffentliches Produkt** (`github.com/greecro/proxmox-perfect-wordpress`): **ein** Script, das
auf einem Proxmox-Host läuft, einen unprivilegierten LXC anlegt und darin
[`greecro/perfect-wordpress`](https://github.com/greecro/perfect-wordpress) ausführt. Interaktiv,
kein Editieren von Dateien nötig. Details: [README.md](README.md) (englisch).

## Projektregeln

1. **Dieses Repo ist nur der Wrapper.** Alles, was *innerhalb* des Containers passiert, gehört
   nach `perfect-wordpress` — hier keine Stack-Logik nachbauen.
2. **Öffentliches Repo, fremde Proxmox-Hosts.** Keine IPs, Gast-IDs, Storage- oder Bridge-Namen
   aus Danys Cluster, auch nicht als Default. Danys eigenes Hosting läuft über
   `wp-hosting-scripts`, nicht über dieses Script.
3. **Debian-13-Templates sind minimal.** `sudo` fehlt und muss vorinstalliert werden, und die
   Locale muss *richtig* erzeugt werden — eine fehlende Locale war die Ursache eines
   Redis-Absturzes, nicht Redis selbst. `apt` mit `LANG=C` aufrufen, damit das
   `locales`-postinst nicht `update-locale` anstößt.
4. **Nach dem Installieren eines Binaries `hash -r`**, sonst findet die Shell es im selben Lauf
   nicht (real passiert bei FileBrowser).
5. **Der Wrapper ist an die Prompts des Installers gekoppelt.** Ändert sich dort etwas, bricht er
   stumm — bei jeder Änderung beide Repos zusammen prüfen.
