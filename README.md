# Power Apps canvas app — versiebeheer

Dit is een lokale Git-basis voor app `151d440a-8600-4911-a870-06865be14af5`
in environment `7aef38fe-c04f-ef38-8408-e3520a13fa50`.

## Huidige status

- `authoring/` bevat een verse MCP-export van de huidige coauthoring-sessie.
- Dit is authoring-broncode, inclusief `_EditorState.pa.yaml`, geen volledige solution-export.
- GitHub-remote: https://github.com/MaximAxxes/PowerAppTest1 (branch main). Er is geen native Dataverse Git-koppeling ingesteld.
- Alleen Git pushen past de app niet aan.

## Werkflow met MCP en Git

1. Begin met een schone Git-werkmap. Haal Git-wijzigingen binnen met `git pull --ff-only`.
2. Vergelijk eventuele Studio-wijzigingen via een MCP-export naar een aparte tijdelijke map; overschrijf lokale wijzigingen niet.
3. Werk op een featurebranch en pas de YAML in `authoring/` aan.
4. Bekijk `git diff`, commit en push de wijziging naar GitHub.
5. Pas de gekozen commit toe met `compile_canvas` op de absolute `authoring/`-map. Deze tool verwerkt wijzigingen in de verbonden app; het is geen offline dry-run.
6. Controleer App Checker en toegankelijkheid. Exporteer opnieuw naar een tijdelijke map om de werkelijk toegepaste broncode te vergelijken.
7. Test de app in Studio. Opslaan en publiceren zijn afzonderlijke releasehandelingen.

Bij een rollback: gebruik `git revert` voor de gewenste commit, bekijk de diff en pas de resulterende YAML opnieuw toe via MCP. Een Git-revert alleen verandert de app niet.

## Native GitHub → Power Apps

De directe integratie loopt via Dataverse Git-integratie en een custom unmanaged solution. Laat Power Platform eerst de solution en app exporteren naar de gekoppelde repository. Gebruik die gegenereerde structuur als basis; maak geen solutionstructuur na uit deze losse authoring-bestanden.

De GitHub-koppeling is volgens de geraadpleegde Microsoft-documentatie een preview. Vereisten zijn een managed Dataverse-developmentomgeving, System Administrator-rechten, een custom unmanaged solution, GitHub-organisatiebeheer, een GitHub App en Azure Key Vault in dezelfde Entra-tenant. De app krijgt Contents Read and write voor de gekozen repository; de sleutel blijft in Key Vault.

Native workflow: gepubliceerde development-app/solution naar Git committen → branch wijzigen → review en merge → changes naar de gekoppelde developmentomgeving pullen → testen. Microsoft ondersteunt kleine directe canvas-YAML-edits, adviseert geen grote wijzigingen en sluit direct bewerken van apps met code components uit.

De MCP-authoring-workflow hierboven kan al versiebeheer geven vóórdat deze native infrastructuur beschikbaar is. Ze is niet hetzelfde als native Dataverse Git-integratie.

## Documentatie

- [Canvas-broncodebeheer](https://learn.microsoft.com/en-us/power-platform/alm/git-integration/canvas-apps-git-integration)
- [GitHub-koppeling en vereisten](https://learn.microsoft.com/en-us/power-platform/alm/git-integration/connecting-to-github)
- [Koppelen via API zonder UI-automatisering](https://learn.microsoft.com/en-us/power-platform/alm/git-integration/git-api)
- [MCP-authoring](https://learn.microsoft.com/en-us/power-apps/maker/canvas-apps/create-canvas-external-tools)

