---
name: kb-article
description: Write or update a WeldKnow knowledge base page from a solved helpdesk conversation, meeting notes, a how-to the user explains, or existing documents, checking first for a page that already covers it. Use when the user asks to document this, write a help article, add this to the knowledge base, or turn a support answer into an article.
argument-hint: <topic, conversation number, or paste the source>
---

# Knowledge base page

Write a WeldKnow page about `$ARGUMENTS`.

1. **Collect the source:** a helpdesk conversation (`search_conversations`,
   then `get_conversation` with `include: messages`), notes pasted in this
   conversation, or what the user explains. Remove customer names, email
   addresses and anything else personal or confidential.
2. **Check what exists:** `list_knowledge_spaces`, then
   `search_knowledge_pages` with the key terms. If a page already covers the
   topic, read it with `get_knowledge_page` and propose an update instead of
   a new page.
3. **Pick the place:** the space, and a parent page from
   `get_knowledge_page_tree` when the space has a structure. Ask when it
   isn't obvious.
4. **Write it** for the reader who has the problem:
   - a title that matches how people search ("Reset two-factor
     authentication", not "2FA info");
   - one line saying who it's for and when it applies;
   - numbered steps, one action each;
   - what to do when it doesn't work.

   Use light markdown only: `#`, `##` and `###` headings, `-` bullets, `1.`
   numbered steps, blank lines between paragraphs.
5. Show the page. On yes, `create_knowledge_page` with `spaceId`,
   `parentId`, `title` and `content`, or `update_knowledge_page` for an
   existing page. Say where it was published.
