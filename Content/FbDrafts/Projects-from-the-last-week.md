# Projects from the last week

I have built a tone of cool things in the last week and /need/ to share them, I plan on writing full blog posts on each, potentially broken into specific topics (infra/archetecture/more boring stuff y'all wont care about) I'm about halfway through a single post and god writing takes time, so i'm just going to dump a bunch of posts here now and expand on them later throughout the week.

That half a blog post really sapped my creative energy and the writeups very quickly turned into a dry list of features, but so be it lol.

Anyway, First up:

# Vault

I have spent the last few weeks building some cool things, a few with deep ai integration. The entire space largely boils down to non-technical people making a bunch of markdown files begging the ai not to do something stupid and people are acting like a repo full of .md files are the next technological breakthrough (I'm looking at you milla jovovich)

I jokingly thought "wow we are about a year away from re-inventing vimwiki from first principles", and then stopped. 

And did exactly that.

AI (atleast ones I can run on my computer) is primarily good for things you could ask a pre-schooler to do (as far as actionable processes) and reasonable expect them to be able to do. Cloud models don't have this issue, but even with all the guardrails and MCP servers asking to check my task list resulted in all the local models doing silly things (like make a file called "path/to/file.csv" for no reason). But they excell at, well, generating text. 

For these projects all the actual logic is done the good-old-fashioned boring way of actually using propper code to handle the logic, and then handing it to the llm only for the resulting user facing interface.

IE: people spending $5 to have open-claw check their inbox only for it to get side tracked and sending your ex an email saying you miss them, the thing that /actually/ makes the most sense is the have the logic handled functionaly and the end result interfaced with an llm

I have used/tried out virtually every note app/platform and kept ending up with notion (for it's availibility) and local project level notes with a cronjob to handle symlinking and a keybound macro to generate a daily scratchpad for ephemeral notes throuout the day, along with a slew of task managment platform and scripts to keep them in sync. So I knew what features I wanted availible, and baked them all in.

### Features:
- Fully writen in go and svelte (purely because I have never used it before)
  - The resulting front-end is bundled into the built go binary, so the entire program including 2 webservers and the front end is a single 50mb file
  - decided to dockerize an instance so that I can run it as a webserver behind traefik as a reverse proxy and have it availible from my phone over a wireguard vpn 
- Daily Overview, Day planning/Intention setting
- Task and Habit Managment
- "Inbox" jotted quick note capture
- Medium term Project, Goals, Deadlines and Vison alignment with manual and AI bases (a bunch of boring math and pattern matching to check burndown rates/task completion) and rollup
- Full calendar, drag and dop scheduling modes etcetc
- AI:
  - Fully provider configurable, designed to be fully functional using an extreamly small local model I'm rather fond of (700mb!), which while rather personable is functionaly retarded if you ask it to do any actions on data.
  - Integration surfaces are delibratly limited to "user information" surfaces, anything that requires any actual logic is handled by boring (but consistent) backend go functions.
  - Pre-Configured flows for agent runs
  - Auto-Generation of tags, summaries and interactive "argument" over current file. 
- Full Markdown editor (with vim keybinds!)
  - Vector Embedding over notes for extreamly fast semantic searches and zettelkasten-esque note linking - I was considering using elasticache as the backend for this, but it's much too heavy and went with rolling my own encoding for storing blobs at a project level to keep the overheads low
  - Live preview
  - Slideshow mode
  - "Generate" command for building and deploying project level documentation as a github pages site
- Markdown Template Managment
- "Vault Project Init" Command
  - Creates Hard-Linked dot folder/files that are both in the project and in the main vault, handles association of project level tasks, notes and sets up git tracking/internal project managment
  - Allows for association of project level tasks with external task provider (todoist/Linear/Github issues) and sets up a two-way sync to a markdown file
  - Surfaces association of git project/location/status/branch (I have many duplicate copies of repos that diverge entirely on my machine)
  - Pasting an image will automatically handle upload and embedding a markdown safe image link
- Object API - I was considering using atomic-server or dnote for producing structured data for interoperability, rolled my own serialiser instead
- CLI commands for things I want to do in the terminal
  - Add tasks/reminders/quick notes
  - Handle multiple simultaneus vaults
  - Bootstrap new vaults
- Full TUI
  - I was more or less rebuilding my vimwiki config from the ground up, so why not /Actually/ rebuild it
  - Kinda busted lol, works fine on my machine in a real terminal emulator (kitty) but shits the bed drawing multiple virtual windows over ssh from the windows terminal (expected, windows is shit)
- A bunch of other stuff I can't be bothered writing about