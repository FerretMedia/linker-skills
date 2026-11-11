# Linker for Claude

Design, set up and grow your [Linker](https://linker.cool) link-in-bio page
from Claude. This plugin brings the Linker connector, which reads and changes
your page, together with skills that teach Claude how to do the work well:
pick a look that fits, write CSS that passes Linker's checks, plan a launch,
read your numbers, keep your clients and build widgets.

## Skills

| Skill | What it does | Plan |
| --- | --- | --- |
| `page-design` | Restyles your page from a description: colours, fonts, buttons, header, picture frame, animated background, or a ready-made look. Undoes it on request. | Pro |
| `page-css` | Writes custom CSS for what the Look settings can't do, within the rules Linker's CSS tab checks, and fixes CSS it flagged. | Pro (free when you paste it yourself) |
| `page-setup` | Writes your name and description, orders and groups your links, and reviews a page that has grown messy. | Pro |
| `launch` | Puts a launch first on your page, makes a tracked link per platform, reports which one worked, and puts the page back afterwards. | Pro, tracked links on Max |
| `page-report` | A short report on visits, link clicks, sources and TikTok posts, with one to three things to change. | Max |
| `media-kit` | A media kit, brand pitch or sponsor recap built on your real numbers. | Max |
| `client-onboarding` | Adds a client, starts them on a workflow and makes their client page link. | Max |
| `client-follow-ups` | Finds who needs a reply or a nudge today, drafts the messages and updates their stage. | Max |
| `widgets` | For a business: writes, fixes and publishes the widgets it offers to creators' pages (a rating, a menu, an event), fixing whatever Linker's widget checker finds. | Pro (free when you paste the files yourself) |

## Use it

1. Add the plugin, then connect **Linker** from the plugin's Connectors tab and
   sign in with your Linker account. In Claude Code:
   `claude plugin marketplace add FerretMedia/linker-skills`, then
   `claude plugin install linker@ferret-media`.
2. Ask in your own words: "give my page a retro arcade look", "I'm releasing a
   single on Friday, set my page up for it", "how did my page do this month?",
   "who do I need to get back to?".

The connector comes with Linker's paid plans: on Pro, Claude reads and changes
your page; on Max and Ultra, it also reads your numbers and keeps your
clients. On the free plan the tools explain that and change nothing. Which
plan includes what: <https://linker.cool/docs/ai-connector#plans>.

If your account is in more than one organization, pick the one Claude works on
in Linker's Settings → AI connector.

## Data

The skills are instructions only: they run no code and send nothing anywhere.
Everything the plugin reads or changes goes through the Linker connector at
`https://mcp.linker.cool/mcp`, signed in as you, to your own Linker account.
That covers your page (name, description, links, look, custom CSS), and on
Max and Ultra your page's statistics, tracked links and clients' details when
you ask about them. Linker's privacy policy: <https://linker.cool/legal/privacy>.

You can switch every AI app off at once in Linker's Settings → AI connector.

## Help

<https://linker.cool/docs/ai-connector#help>, or hello@linker.cool.

## License

MIT, see [LICENSE](LICENSE).
