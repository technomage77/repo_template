# repo_template

## Workflow

Um von Anfang an die Best Practices mit **CodeQL** und **OpenSSF Scorecard** konsistent in GitHub-Projekten umzusetzen und diese als Template für weitere Repositories nutzbar zu machen, empfiehlt sich folgende Vorgehensweise:

### Initiale Umsetzung in einem Basistemplate

- Richte ein dediziertes Repository für templates oder ein "baseline"-Starter-Repository ein.
- Lege darin die .github/workflows für **CodeQL** (z.B. `codeql.yml`) und **OpenSSF Scorecard** (z.B. `scorecard.yml`) ab.[1][2][3]
- Ergänze die README.md direkt mit Badges für beide Tools, z.B.
  ```
  [![OpenSSF Scorecard](https://api.scorecard.dev/projects/github.com/{OWNER}/{REPO}/badge)](https://scorecard.dev/viewer/?uri=github.com/{OWNER}/{REPO})
  ```
- Dokumentiere darin auch relevante Policy-Dateien und empfohlene Einstellungen (Branch Protection, 2FA, Dependabot etc.) für weitere Projekte.[4][1]

### Umsetzung und Wiederverwendung mit GitHub Features

- Nutze **GitHub Repository Templates** (Checkbox "Use as a template"), um neue Repos direkt mit diesen Workflows und Einstellungen auszustatten. Für Organisationen empfiehlt sich ein zentrales Baseline-Repo.[5][4]
- Alternativ kannst du die Workflows als **wiederverwendbare GitHub Actions Workflows** definieren (siehe `.github/workflows/`), sodass andere Repos diese über `uses:` referenzieren und so zentral Änderungen erhalten, z.B.
  ```yaml
  jobs:
    codeql-analysis:
      uses: orgname/workflows/.github/workflows/codeql.yml@main
  ```
  oder
  ```yaml
  jobs:
    scorecard:
      uses: orgname/workflows/.github/workflows/scorecard.yml@main
  ```
  Dabei lassen sich Secrets und Konfigurationen an den Aufrufer delegieren.[6][7][8][4]

### Empfohlene Praxis und Hinweise

- Passe die Workflows so an, dass sie für verschiedene Sprachen und Build-Umgebungen leicht portierbar sind – z. B. über Matrix-Strategien.
- Halte Workflows und Policy-Dateien im Template-Repo aktuell, damit nach neuen Projekterstellungen stets aktuelle Security-Standards gelten.
- Dokumentiere im Template ausführlich, wie und warum Scorecard und CodeQL genutzt werden – das erleichtert die Einführung für neue Teammitglieder und Community-Contributor.[1][5]
- Auch bestehende Repos lassen sich mit diesen Workflow-Dateien und der README-Konvention nachrüsten.

Damit kann in jedem neuen Projekt sofort einheitlich und transparent der aktuelle Security-Status angezeigt und relevante Sicherheits-Automatisierung aktiviert werden.[7][5][6][4][1]

[1](https://github.com/ossf/scorecard)
[2](https://notes.kodekloud.com/docs/GitHub-Actions-Certification/Security-Guide/Use-CodeQL-as-a-step-in-a-workflow)
[3](https://github.com/ossf/scorecard-action)
[4](https://docs.github.com/en/actions/concepts/workflows-and-actions/reusable-workflows)
[5](https://techcommunity.microsoft.com/blog/azuredevcommunityblog/enhancing-security-and-scalability-with-reusable-workflows-in-github-and-pipelin/4200152)
[6](https://docs.github.com/en/actions/how-tos/sharing-automations/reusing-workflows)
[7](https://github.com/actions/reusable-workflows)
[8](https://stackoverflow.com/questions/71524542/how-to-use-reusable-github-workflows-and-keep-secrets-in-a-single-place)
[9](https://github.com/erlang/otp/issues/8922)
[10](https://github.com/ossf/wg-best-practices-os-developers)
[11](https://scorecard.dev)
[12](https://devblogs.microsoft.com/dotnet/openssf-scorecard-for-net-nuget/)
[13](https://www.coalitioninc.com/blog/security-labs/centralizing-security-automation-github-reusable-actions)
[14](https://dev.to/nodesecure/securize-your-github-org-4lb7)
[15](https://docs.github.com/en/actions/how-tos/reuse-automations/reuse-workflows)
[16](https://arxiv.org/pdf/2208.03412.pdf)
[17](https://github.blog/developer-skills/github/codeql-zero-to-hero-part-2-getting-started-with-codeql/)
[18](https://github.com/ossf/scorecard-monitor)
[19](https://docs.github.com/en/actions/reference/security/secure-use)
[20](https://scorecard.dev/viewer/?uri=github.com%2FStefanSchroeder%2Fttfsample)
