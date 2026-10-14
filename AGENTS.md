# AGENTS.md – Arbeitsregeln für KI-Coding-Agenten

> **English summary:** Do **not** open pull requests in this repository. Commit to
> your working branch and push. The GitHub Action
> `.github/workflows/auto-merge-arena.yml` merges every push on `arena/**` into
> `main` automatically within about a minute.

## Die eine Regel

**Erstelle keine Pull Requests. Push genügt.**

Dieses Repository hat einen Auto-Merge-Workflow: Jeder Push auf einen Branch,
der mit `arena/` beginnt, wird von GitHub automatisch nach `main` gemerged –
ohne PR, ohne Review, ohne Rückfrage. Frag nicht nach Freigabe, warte auf
keinen Merge, erstelle keinen PR „zur Sicherheit“.

| Tu das | Lass das |
|---|---|
| Regelmäßig committen und pushen (`git push origin <dein-branch>`) | PRs anlegen, auf Merge warten, nach Freigabe fragen |
| Vor jedem Push prüfen, ob der Stand lauffähig ist (Syntax, Tests) | Halbfertige Zwischenstände pushen – sie sind sofort in `main` und ggf. live |
| Am Ende der Session den Abschnitt „Projektstand“ unten aktualisieren | Arbeit uncommitted liegen lassen – nur Gepushtes überlebt die Session |

## Ablauf pro Arbeitsschritt

1. Änderung umsetzen und lokal prüfen.
2. `git add -A && git commit -m "<typ>: <was und warum>"`
3. `git push origin <dein-branch>`
4. Fertig – nach ca. einer Minute ist der Stand in `main`.
   Kontrolle (optional): `gh run list --workflow=auto-merge-arena.yml --limit 3`
   oder `git fetch origin main && git log --oneline -3 origin/main`

## Wenn der Auto-Merge fehlschlägt

- **Merge-Konflikt** (parallel wurde auf `main` gepusht):
  `git fetch origin && git merge origin/main` → Konflikte lösen → committen → erneut pushen.
- **403 / Permission denied:** Nicht dein Problem – bitte den Nutzer,
  *Settings → Actions → General → Workflow permissions → „Read and write“* zu prüfen.
- **Workflow startet gar nicht:** Dein Branch-Name passt nicht auf `arena/**`.
  Nenne dem Nutzer das Muster, das er in der Workflow-Datei ergänzen soll.

## Grenzen

- Dateien unter `.github/workflows/` kannst du nicht pushen (der Agent-Token hat
  keine `workflows`-Berechtigung). Vorschläge dafür an anderer Stelle ablegen
  (z. B. `ci/`) und dem Nutzer den Zielpfad nennen.
- Keine Secrets, Tokens oder Passwörter in Dateien oder Commits.

## Projektstand (vom Agenten am Session-Ende pflegen)

<!-- Kurz halten: Was muss ein neuer Agent in 60 Sekunden wissen? -->

- **Was ist das hier:** _(ein Satz)_
- **Stack / Start / Test:** _(Sprache, Framework, Befehle)_
- **Zuletzt erledigt:** –
- **Offen / nächste Schritte:** –
- **Stolperfallen:** –
