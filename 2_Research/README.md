# 2_Research

Research your agent collects for you, in dated folders so it stays easy to browse and clean up.

| Folder | Holds | Name |
|---|---|---|
| `Reports/YYYY/MM/` | One-off reports and collected findings | `YYYY-MM-DD <topic>.md` |
| `News/YYYY/MM/` | News articles found about contacts, by `outreach-news` | `YYYY-MM-DD <Company or Person> - <headline>.md` |
| `News/Archive/` | News older than three months, moved by `monthly-cleanup` | Same as above |

Every file starts with its source and the date it was found. Articles are saved as short summaries with a link,
not full copies.

`News/` is gitignored, because it shows who the user is in touch with. Reports are shareable.

The `util-files` skill files reports here. `outreach-news` files news here.
