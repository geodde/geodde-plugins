---
name: write-geodde-page
description: Write one page for a Geodde site end to end — pick the top topic on the content roadmap, claim it, read the page brief, research the web, write every section, and send the draft back to Geodde for review. Use when asked to write, draft or create content for a Geodde site, or to work through the Geodde content roadmap. Needs the Geodde connector (MCP server at https://app.geodde.com/mcp).
---

# Write a Geodde page

Geodde tracks how AI assistants (ChatGPT, Claude, Gemini, Google AI Mode) answer the questions a business's buyers ask, and plans the pages that would get the business cited. This skill writes one of those pages and hands it back to Geodde. It never publishes: a person reviews and publishes in Geodde.

All tool names below are tools on the Geodde connector.

## 1. Pick the site

If the user named a site, use it. Otherwise call `list_sites`. If there's more than one, ask which. Pass its id as `site_id` to every call below.

## 2. Pick a topic

Call `content_roadmap`. Take the first row in `items` unless the user asked for something else. Skip anything listed in `drafting` — another writer already has it.

Check `data_as_of`. If it's more than two weeks old, tell the user the roadmap may be stale before going on.

## 3. Claim it

Call `create_page` with the row's `topic_id` and a short `brief`: the topic's label and the angle you'll take. This links the page to the topic so nobody else picks it.

If it refuses because the topic is taken, go to the next roadmap row (at most three tries). Keep the `page_id` and `url` it returns.

## 4. Understand what the page must do

- Call `topic_detail` with the topic id. Its `fanout_searches` are the queries AI assistants run when answering these questions — the page has to answer them.
- Call `page_brief` with the `page_id`. It lists the `sections` to write (each with a slug, purpose and target length), the prompts the page must answer, the brand facts to use, and the writing rules. Follow the writing rules.

## 5. Research

Search the web for the main fan-out searches. Read the pages that rank and the pages AI assistants cite. Note what they cover, what they miss, and the source of any fact you'll use.

## 6. Write

- Write every section `page_brief` lists, in markdown, close to its target length.
- Answer the prompts directly and early.
- Use the brand facts. Facts in the `competitor` category are about competitors, not this business.
- Never invent facts, statistics, customers or quotes. Leave something out rather than guess. If two brand facts contradict each other, use neither.
- Write in the business's own voice.

## 7. Send it back

Call `submit_content` with the `page_id`, one entry per section (`slug` and `markdown`), and the `brief` you wrote from. If it refuses, fix what it names and try once more.

## 8. Report

Tell the user the page title, the topic, the `url` from `submit_content`, whether it was sent for approval, and anything you left out or weren't sure of — including any contradicting brand facts.
