# South Sudan: law history in git

The law of South Sudan as a git history: one file per provision (article, section or schedule), one commit per version on the day it took effect, and the act that made each change as the commit's author. `git blame` names the act behind every paragraph; `git log` lists every change to a provision; picking a date gives the text in force that day.

Part of [lexifina/global-law](https://github.com/lexifina/global-law), one git history for every country's law: this is South Sudan's national law, which global-law reads at `south-sudan/national/acts/`.

**What is in it now:** 3 acts, each as enacted, in one version: the Transitional Constitution of the Republic of South Sudan, 2011 (203 articles, the preamble, 5 schedules and the President's assent), the Penal Code Act, 2008 (Act 9 of 2008) and the Code of Criminal Procedure Act, 2008 (Act 5 of 2008). [`REPRODUCE.md`](REPRODUCE.md) lists each act and every decision made in building it; [`data/laws.csv`](data/laws.csv) gives each act's dates and source.

Each act is a folder, one file per provision, plus a `README.md` listing its provisions (`constitution/art-001.md` is Article 1 of the Constitution, the Republic of South Sudan and its territory; the codes are in `penal-code/` and `criminal-procedure/`).

The text is in English, the language South Sudan's laws are published in, as the Ministry of Justice and Constitutional Affairs prints it.

## Questions as git commands

| Question | Command |
| --- | --- |
| Every change to Article 1 of the Constitution | `git log -p --word-diff -- constitution/art-001.md` |
| Which act wrote each line of Article 1? | `git blame constitution/art-001.md` |
| Every version of the Constitution, with the day each took effect | `git log --format="%h %(trailers:key=In-force,valueonly,separator=) %an" -- constitution ':!*/README.md'` |
| Article 1 as in force on 1 January 2012 | `python tools/on.py 2012-01-01 constitution art-001` |

**Outside git**, we also host this record publicly, for free:

- **[Ask Claude about South Sudanese law](https://global-law.lexifina.com/v1/try_claude?country=south-sudan)**: opens Claude with a first question ready.
- **[Ask ChatGPT](https://global-law.lexifina.com/v1/try_chatgpt?country=south-sudan)**: the same question in ChatGPT.
- **[Search South Sudanese law on our site](https://lexifina.com/law?country=south-sudan&q=bail)**: a search for "bail", with each provision's text and its versions, no account needed.
- **[Developer REST API](https://global-law.lexifina.com/v1/search_law?query=bail&jurisdiction=south-sudan)**: the same search as JSON, with no key. See the [documentation here](https://lexifina.com/api/global-law).

Both assistants read the record through the free Global law connector (MCP, `https://global-law.lexifina.com/mcp`); the first time, the chat gives you the link that adds it. Ask in English.

**Host it yourself easily.** All it takes is git and Python, and the tools run on your machine:

```sh
git clone --depth 1 https://github.com/lexifina/global-law && cd global-law
python3 tools/countries.py add south-sudan/national/acts
python3 tools/law.py show 2012-01-01 south-sudan/national/acts/constitution/art-001.md
```

Opened in Claude Code, Cursor, VS Code or Codex, the clone also starts a local MCP server with the same tools ([MCP.md](https://github.com/lexifina/global-law/blob/main/MCP.md)).

## Dates

Each commit is dated at noon, Africa/Juba, on the day the version took effect, and carries it in its `In-force:` trailer. The dates come from the texts themselves:

- the Penal Code Act and the Code of Criminal Procedure Act come into force on the President's signature (section 1 of each), dated by the "Signed on" margin note of their gazette print: 22 August 2008 and 20 March 2008. Both were published on 10 February 2009 (a `Published:` trailer);
- the Constitution comes into force on 9 July 2011 (Art. 198). Its assent formula leaves the day blank and is kept as printed.

There are no amending acts here, so each act is one commit credited to the act itself (`Penal Code Act 2008 <pca-2008@mojca.invalid>`), and `git blame` names that act for every line.

## How it is checked

- `tools/check_repo.py` reads every version back from git on the day it took effect and on the day before, and compares it with the corpus the history was built from; every commit's trailers must parse, and there are no merge commits, no commit dates that go backwards and none in the future.
- Each version records the sha256 of the ministry PDF it was read from ([`data/versions.json`](data/versions.json)); `tools/build.py` gives the same commit hashes from the same corpus.
- [`REPRODUCE.md`](REPRODUCE.md) does not yet record a run of the check or a second build.

## What it does not show

- **The Constitution as in force today.** It was amended by an Act of 2013 (in force 1 March 2013), published only as a scan with no text layer, and again by 2015 and later, with no official text found; none of these amendments is here.
- **Amendments to the two codes.** The ministry's list offers no amending act or consolidated text for either; an amendment not on that list is not here.
- **The rest of South Sudanese law.** The ministry lists about 80 laws; the Labour Act 2017 and the Companies Act 2012 were looked at but not built. There is no subordinate legislation, case law or bill.
- **Part and chapter structure.** Headings and the arrangement of articles and sections are left out, though 23 files still end with the chapter heading that follows them.
- **Seven sections as files of their own.** Penal Code sections 76, 111, 135, 151 and 335 and Code of Criminal Procedure sections 130 and 305 run on at the end of the section before them.

## Sources

| Source | Kind | Past versions | Notes |
| --- | --- | --- | --- |
| [Ministry of Justice and Constitutional Affairs](https://mojca.gov.ss/laws-of-the-republic-of-south-sudan/): Laws of the Republic of South Sudan | Official texts as enacted (PDF) | no, one text per act | Not consolidated. The site's certificate has expired, so each text is read from an [Internet Archive](https://web.archive.org/web/20260727084226/https://mojca.gov.ss/laws-of-the-republic-of-south-sudan/) capture of the ministry's PDF |
| [WIPO Lex](https://www.wipo.int/wipolex/en/legislation/details/11412) (World Intellectual Property Organization) | Records of the Constitution and its 2013 amendment | no | Only the records' dates and notes are used, not WIPO's texts |

## Licence

See [`LICENSE`](LICENSE). The texts are laws of the Republic of South Sudan as the ministry publishes them, copied unaltered apart from layout and attributed to it; the ministry's rights notice ("All Rights Reserved") is recorded in `LICENSE` in full. The arrangement of the history, the commit messages and the tools are Lexifina's, under CC BY 4.0.

No AI model wrote, translated or corrected legal text, and none runs when the history is built; the scripts were written by an AI model (see [`REPRODUCE.md`](REPRODUCE.md)).

## More

From [lexifina/global-law](https://github.com/lexifina/global-law):

- [FEATURES.md](https://github.com/lexifina/global-law/blob/main/FEATURES.md): every feature, and what every corpus must support (`git blame`, `law.py`, the MCP tools)
- [FAQ.md](https://github.com/lexifina/global-law/blob/main/FAQ.md): questions and answers · [CONTRIBUTING.md](https://github.com/lexifina/global-law/blob/main/CONTRIBUTING.md): proposing changes · [MCP.md](https://github.com/lexifina/global-law/blob/main/MCP.md): the MCP server · [REPRODUCE.md](https://github.com/lexifina/global-law/blob/main/REPRODUCE.md): how it was built · [CHANGELOG.md](https://github.com/lexifina/global-law/blob/main/CHANGELOG.md)
- [FRESHNESS.md](https://github.com/lexifina/global-law/blob/main/FRESHNESS.md): how current each corpus is · [Monitoring](https://github.com/lexifina/global-law/tree/main/monitoring): whether updates are running · [WATCHING.md](https://github.com/lexifina/global-law/blob/main/WATCHING.md): how each official source is watched for changes
- [performance/](https://github.com/lexifina/global-law/tree/main/performance): how fast the tools are, measured
- [visualisations/](https://github.com/lexifina/global-law/tree/main/visualisations): charts and bridges across the world's law
- [Vulnerabilities](https://github.com/lexifina/global-law/tree/main/vulnerabilities): mistakes in legislation as published
