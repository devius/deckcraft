# Georgian interface

> **Last reviewed:** 2026-10-17 · **Last updated:** 2026-10-27 · **Change:** minor (upstream sync: 1,568 entries, Noto Sans Georgian from craft-fonts; previous: minor, upstream sync: 1,451 entries; Georgian in Review › Language and Date and Time; previous: minor, Georgian interface notes and terminology) · **Target:** DeckCraft 0.6.1

Choose **Review › Language** or **Preferences… (Cmd+,) › Interface language › ქართული**, or follow a
Georgian system locale (`ka`, `ka-GE`, `ka_GE.UTF-8`; the system choice is read through
`sys_locale` when the preference is **System language**). The catalog code is `ka`; the control and
MCP command `app.language` with `{"language":"ka"}` selects it explicitly. The choice is saved with
the other interface settings. Slide text, command ids, CLI/MCP/control responses and file paths do
not change.

`crates/ui-egui/src/i18n/ka.tsv` has 1,568 entries: all 1,232 keys of the Ukrainian catalog plus 336 labels upstream added since
(File › Print/Info, IME commands, new preset shapes, transition Effect Options, SmartArt, Edit
Points, guides, motion paths, presenter controls, Find and Replace, Photo Album). It
covers the ribbon tabs and commands, menus, dialogs, panes, the shape and gallery names, and status
captions. Diagnostics from lower layers (file import, rendering, media) keep their English wording,
as in the other languages. It is written from the meaning of the English labels; no proprietary
translation resources were consulted.

## Georgian script

- **No case.** Mkhedruli has no upper and lower case. Change Case › Sentence case and Capitalize
  Each Word leave Georgian letters alone; UPPERCASE and Toggle Case follow Unicode and give Mtavruli
  (`ᲐᲑᲒ`). The interface never uses Mtavruli, and commands are verbal nouns (`შენახვა`, `ჩასმა`).
- **Counts** are count-neutral: the noun comes first and stays singular (`სლაიდი: 5`), so `count()`
  takes a single Georgian form.
- **Dates:** short date fields use `dd.mm.yyyy`; Insert › Date and Time lists Georgian (`ka-GE`).
- **Proofing language:** Review › Language lists ქართული (`ka-GE`) for marking Georgian text.
- **Fonts:** builds with craft-fonts embed Noto Sans Georgian and put it ahead of the bundled Hack
  fallback (whose monospaced Georgian draws the interface otherwise). Slide text uses the font
  database's per-character fallback (#101). The web (WASM) build embeds no Georgian face; the page
  fetches `fonts/NotoSansGeorgian.ttf` from beside itself when the site serves it.

## Terminology

| Source | Georgian |
|---|---|
| Home (ribbon tab) | მთავარი |
| Insert / Paste | ჩასმა |
| Design / Themes | დიზაინი / თემები |
| Transitions / Animations | გადასვლები / ანიმაციები |
| Slide Show / From Beginning | სლაიდშოუ / დასაწყისიდან |
| Review / Spelling | განხილვა / მართლწერა |
| View / Normal | ხედი / ჩვეულებრივი |
| New Slide / Duplicate Slide | ახალი სლაიდი / სლაიდის დუბლირება |
| Slide Master | მასტერ-სლაიდი |
| Slide Sorter | სლაიდების დამხარისხებელი |
| Presenter View | მომხსენებლის ხედი |
| Notes / Notes Page | შენიშვნები / შენიშვნების გვერდი |
| Layout | განლაგება |
| Shapes / Format Shape | ფიგურები / ფიგურის ფორმატირება |
| Shape Fill / Shape Outline | ფიგურის შევსება / ფიგურის კონტური |
| Picture / Chart / Table | სურათი / დიაგრამა / ცხრილი |
| Text Box | ტექსტური ბლოკი |
| Font / Paragraph | შრიფტი / აბზაცი |
| Change Case | რეგისტრის შეცვლა |
| Undo / Redo | დაბრუნება / ხელახლა შესრულება |
| Slide Size | სლაიდის ზომა |
| Hide Slide / Rehearse Timings | სლაიდის დამალვა / დროის გაზომვა |
| Link / Comments | ბმული / კომენტარები |
| Section | სექცია |
| Edit Points / Size and Position… | წერტილების რედაქტირება / ზომა და პოზიცია… |
| Grid Options… / Guides | ბადის პარამეტრები… / დამხმარე ხაზები |

Please follow this table and the shared ArtCraft Georgian glossary when you add strings. Product and
format names stay as they are.

## Verification and maintenance

Add a string to `crates/ui-egui/src/i18n/ka.tsv` as `English source<TAB>Georgian` (`\n` for a line
break), next to the same key in the other catalogs. Keep placeholders (`{}`, `{n}`), ellipses and
`\n` breaks exactly; strings added later fall back to English until they are translated.

`cargo test -p deckcraft-ui-egui --lib i18n` checks that every catalog has the same keys, that
placeholders match, that every command, menu, gallery and literal `tr()` label has an entry, the
`ka`/`ka-GE` locale detection and saved preference, unchanged document data, and that the UI font
draws Georgian (with craft-fonts: Noto Sans Georgian before Hack). The ignored test
`i18n::tests::translated_interface_preview` (run with `DECKCRAFT_I18N_SHOTS=<dir>`) renders the
editor, Preferences and Table dialogs in every language for a visual check. A native-speaker skim
is welcome.

## Revision history

| Date | Change | Summary |
|---|---|---|
| 2026-10-27 | minor | Upstream sync: 1,568 entries; Noto Sans Georgian from craft-fonts replaces the installed-font search |
| 2026-10-17 | minor | Upstream sync: 1,451 entries; Georgian in Review › Language and Date and Time; View is ხედი |
| 2026-10-13 | minor | Georgian interface notes and terminology |
