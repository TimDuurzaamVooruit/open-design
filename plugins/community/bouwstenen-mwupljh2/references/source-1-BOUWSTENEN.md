# Bouwstenen

Bron: laag 2 van `plan.md` en bestaande bestanden in `src/components/ui`. De schets toont vier knopsoorten; het plan noemt er drie. Beide hebben twee maten. Deze inventaris houdt de vier bestaande schetssoorten aan, inclusief gevaar.

Telling: per patroon `rg -l -P <patroon> src --glob *.tsx --glob !*.test.* --glob !*.spec.* --glob !**/__tests__/** --glob !**/ui/**`. Elke bestandsmatch telt eenmaal. Alleen niet-test-TSX buiten `src/components/ui` is geteld. Dit is een ruwe telling van kandidaten voor eigen varianten, geen bewezen duplicaatmeting. Meerregelige attributen en dynamische klassen kunnen ontbreken; een native element kan ook zonder eigen stijl voorkomen. Nul betekent alleen geen match.

| Bouwsteen uit laag 2 | Gedeeld component in src/components/ui | Bestanden met eigen variant, ruw | Zoekpatroon (PCRE) |
| --- | --- | ---: | --- |
| Knop (soorten en maten) | Button.tsx, IconButton.tsx | 129 | `<button\b` |
| Invoerveld | Field.tsx, TextInput.tsx, NumberInput.tsx, Textarea.tsx | 67 | `<(?:input\|textarea)\b` |
| Keuzelijst | Select.tsx | 44 | `<select\b` |
| Datum | DateInput.tsx, DateTimeInput.tsx | 9 | `\btype=[\x22\x27](?:date\|datetime-local\|month)[\x22\x27]` |
| Zoekveld | SearchField.tsx | 3 | `\btype=[\x22\x27]search[\x22\x27]\|<input\b[^>]*(?:[Zz]oek\|[Ss]earch)` |
| Tabbladen | Tabs.tsx (Tabs, HeaderTabs, TabPanel) | 8 | `role=[\x22\x27]tablist[\x22\x27]\|className=[\x22\x27][^\x22\x27]*\btabs\b` |
| Tabel met rij-acties | DataTable.tsx, ActionMenu.tsx, DropdownMenu.tsx | 8 | `<table\b` |
| Kaart | Card.tsx, Page.tsx (Panel) | 51 | `className=[\x22\x27][^\x22\x27]*\bcard\b` |
| Statuslabel | Badge.tsx, StatusBadge.tsx | 22 | `className=[\x22\x27][^\x22\x27]*\b(?:badge\|status-label)\b` |
| Venster | Dialog.tsx, OverlayDialog.tsx, ConfirmDialog.tsx | 13 | `<dialog\b\|role=[\x22\x27](?:dialog\|alertdialog)[\x22\x27]` |
| Zijpaneel | Sheet.tsx | 5 | `className=[\x22\x27][^\x22\x27]*(?:drawer\|sheet)` |
| Lege toestand | DataStates.tsx (EmptyState), templates/PageState.tsx | 47 | `className=[\x22\x27][^\x22\x27]*(?:empty\|no-results)` |
| Laadtoestand | Skeleton.tsx, DataStates.tsx (TableSkeleton) | 27 | `className=[\x22\x27][^\x22\x27]*(?:skeleton\|loading\|spinner)` |
| Foutmelding | DataStates.tsx (ErrorState), PanelNotice.tsx | 150 | `role=[\x22\x27]alert[\x22\x27]` |
| Paginakop met titel, tabs en knoppen | Page.tsx (PageHeader), RecordHeader.tsx, Tabs.tsx | 17 | `<h1\b` |
| Periodekeuze | PeriodPicker.tsx | 2 | `<(?:select\|button)\b[^>]*(?:[Pp]eriode\|[Pp]eriod)\|className=[\x22\x27][^\x22\x27]*(?:period-picker\|period-select\|period-control)` |

## Nieuwe bouwstenen in de startbestanden

Alle aanvullingen staan na de letterlijk gekopieerde schets-CSS. Ze gebruiken dezelfde tokens. Er worden geen React-componenten toegevoegd.

| NIEUW-commentaar | Sjablonen | Doel |
| --- | --- | --- |
| Responsieve schil en toegankelijkheid | `sjabloon-agenda.html`, `sjabloon-beheer.html`, `sjabloon-bord.html`, `sjabloon-cijfers.html`, `sjabloon-dossier.html`, `sjabloon-formulier.html`, `sjabloon-lijst.html`, `sjabloon-werkdag.html` | Gemeenschappelijke schil, focus, tekstomloop en formuliertekst. |
| Laadtoestand | `sjabloon-agenda.html`, `sjabloon-beheer.html`, `sjabloon-bord.html`, `sjabloon-cijfers.html`, `sjabloon-dossier.html`, `sjabloon-formulier.html`, `sjabloon-lijst.html`, `sjabloon-werkdag.html` | Vaste laadregels voor alle hoofdblokken. |
| Leesbare waarschuwingsstatus | `sjabloon-agenda.html`, `sjabloon-beheer.html`, `sjabloon-bord.html`, `sjabloon-cijfers.html`, `sjabloon-dossier.html`, `sjabloon-formulier.html`, `sjabloon-lijst.html`, `sjabloon-werkdag.html` | Waarschuwingstekst gebruikt de bestaande donkere teksttoken voor voldoende contrast. |
| Agendaraster | `sjabloon-agenda.html` | Weekkolommen met afsprakenlijst op mobiel. |
| Bordkolommen | `sjabloon-bord.html` | Fasekolommen op desktop, verticale fasen op mobiel. |
| Cijfergrafiek en doelbalk | `sjabloon-cijfers.html` | Cumulatieve omzet, productverdeling en voortgang. |
| Formulierkolommen | `sjabloon-formulier.html` | Klantgegevens en verkoopcontext naast woning en energie. |
| Veldgroep | `sjabloon-formulier.html` | Bestaande productinteresse als één veldgroep. |
| Werkdagkolommen en actieregels | `sjabloon-werkdag.html` | Actielijst met afspraken en signalen ernaast. |

## Impeccable en broncontrole

Commando: `IMPECCABLE_LAUNCHER_PROBE=1 /Users/timkuiper/.agents/skills/impeccable/scripts/impeccable detect --json frontend-startmateriaal/*.html`. De lokale detector is gebruikt; downloaden was uitgeschakeld. Eerste controle: 8 lettertypewaarschuwingen en 4 contrastadviezen. Het advies betrof waarschuwingslabels op lijst en dossier, gemeten op 4,4:1. De aanvullende regel `.badge.warn{color:var(--fg)}` verhelpt dit met een bestaande token. Hercontrole: exitcode 2, alleen 8 waarschuwingen `overused-font`, precies één per HTML-bestand. Plus Jakarta Sans blijft behouden omdat de opdracht dit lettertype expliciet voorschrijft. Er blijven geen detectorbevindingen over contrast over; dit vervangt geen browsercontrole.

Modus Operate. Gelezen: de Impeccable-skill, `reference/craft-floor.md`, `reference/critique.md`, PRODUCT.md, DESIGN.md en de DV-designrichtlijnen. Dit is een beperkte beoordeling op broncode binnen de opdracht; er is geen volledige onafhankelijke of gerenderde critique uitgevoerd. Geen subagents ingezet.

Bronbevindingen en verwerking: de werkvoorraadkeuze bevat de bestaande categorieën; het dossier behoudt de vier brontabbladen; het formulier behoudt de bronvelden; rapportage heeft de periodekeuze in de kop; tabellen tonen dezelfde velden als mobiele kaarten; het bord heeft alle contractfases en krijgt een verticale mobiele opbouw; de tabnavigatie werkt ook met pijltjes, Home en End. Native invoer, selecties en details blijven lokaal bruikbaar. Actieknoppen zijn statische voorbeelden, geen functionele app.

Toestanden: alle hoofdblokken hebben leeg en laden; aanvullende fout- en geen-toegangstekst staat onder Toestanden. De schermschil blijft zichtbaar. De formulierpreview is bewust geen werkende opslag of validatie. Voorwaardelijke bronblokken zijn waar nodig zichtbaar gemaakt met DEMO-data; vlaggen en rechten zijn niet live gecontroleerd.

No-ai-slop-check: Nederlandse labels en broninhoud gecontroleerd, geen slogans of versiercijfers toegevoegd. Alle voorbeeldrecords, organisaties en bedragen zijn fictief. De lettertypelink is de enige externe verwijzing in de HTML. De opgelegde schets wint in deze losse startbestanden van oudere interne fonts en tokens; de app zelf blijft onaangeraakt.

Beperking: er is op uitdrukkelijk verzoek geen browser, render, test of build gebruikt. Responsiviteit is alleen in HTML/CSS vastgelegd op de schetsgrens van 760 px, niet visueel bewezen op 1440 of 390 px.

### Letterlijke stijlbron en drie vaste waarden

Het volledige `:root`-blok en alle oorspronkelijke klasseregels zijn letterlijk behouden. De bron bevat zelf `color:#fff` in `.btn.primary`, `border-radius:999px` in `.badge` en `border-radius:3px` in `.bar`. Daarom kan letterlijk kopiëren niet tegelijk nul vaste waarden buiten `:root` opleveren. Er zijn geen nieuwe vaste kleuren, tekstgroottes of afrondingen toegevoegd. `.bar` is wel meegekopieerd maar niet toegepast. Een eventuele omzetting van die drie bronwaarden naar tokens is een besluit voor laag 1.

Bestandscontrole met `rg -n -P '(?:font-size|(?<![-])color|background|border-radius)\s*:\s*(?:#[[:xdigit:]]+\b|[0-9.]+(?:px|rem|em)\b|(?:rgb|rgba|hsl|oklch)\()' frontend-startmateriaal/*.html`: 24 regels, dezelfde 3 bronregels in elk bestand. De aanvullende CSS heeft nul matches. `rg -n http frontend-startmateriaal/*.html`: 8 matches, uitsluitend de lettertypelink. HTML-broncontrole bevestigt unieke ids, bestaande lokale links, geldige tabdoelen en toestanden in alle acht bestanden. Geen em-dashes, externe scripts, pop-ups of nieuw-tabbladlinks aangetroffen.

### Architectuurcheck hoofdstuk 7

1. Bestaande bron: schets-CSS en gedeelde UI-componenten geïnventariseerd; geen applicatielogica toegevoegd.
2. Verversen: niet van toepassing, de HTML heeft uitsluitend lokale DEMO-data.
3. Client/server-regels: niet gewijzigd; bordfasen komen uit het bestaande contract.
4. Toestanden: leeg, laden, fout en geen toegang zijn in alle acht bestanden opgenomen.
5. Gedragstest: niet uitgevoerd, deze opdracht sluit tests expliciet uit.
6. Duplicaten gezien: de ruwe telling hierboven noemt kandidaten; niets buiten deze map aangepast. Kopieën van de schets-CSS zijn bewust nodig voor acht zelfstandige ontwerpartifacts, niet voor de productapp.
