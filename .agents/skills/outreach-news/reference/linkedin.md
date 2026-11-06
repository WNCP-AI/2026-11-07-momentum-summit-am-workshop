# LinkedIn in the browser

Optional and off by default. It catches what news sites miss: a new role, a post the person wrote, a company
update. It runs in the user's own browser, signed in as them, the way they'd check it themselves.

[upgrades.md](upgrades.md) turns it on, only after the user reads the warning below and says yes. The
10-profile cap is the `LinkedIn limit:` line in `## News`.

## Tell the user before turning it on

- LinkedIn's User Agreement prohibits scraping and automated access. This flow is slow, read-only and small to
  stay close to normal use, but it's the user's account and their call. If they're unsure, leave it off.
- It needs a harness that can drive a browser the user is signed in to, such as a browser extension or a hosted
  agent's own browser where the user signs in. If this harness can't, leave it off.
- It never signs in for them. If LinkedIn asks for a login or a check, stop and ask the user.

## Rules

- **Read only.** Never connect, follow, like, comment, message or endorse. Never click "Connect" or "Message".
- **Small.** At most 10 profiles per run, one at a time, with a pause of a few seconds between pages. No searching
  LinkedIn for new people. Only open profiles of existing contacts.
- **Narrow.** Open the person's profile URL from the contact list, or search their exact name and company once.
  Look at their headline, current role and the activity or posts tab for the news window. Then the company page's
  posts, if the person showed nothing.
- **Summaries only.** Save a few lines in your own words and the post URL. Don't copy whole posts, comments, or
  other people's details.
- **Stop on friction.** A captcha, a warning, a "too many requests" page, or a login wall means stop LinkedIn for
  this run and tell the user.

## What counts

Strong: a new role or promotion, a funding or launch announcement, a post about a problem the user's company solves.
Weak: likes, reshares without comment, work anniversaries. Label weak items `no` unless settings say otherwise.
