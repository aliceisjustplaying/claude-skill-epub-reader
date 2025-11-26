# EPUB Reader Skill for Claude Code

A Claude Code skill that enables efficient reading of EPUB ebook files.

## Capabilities

- **Metadata extraction** - title, author, publisher, date, language
- **Table of contents** - view chapter structure
- **Chapter reading** - read specific chapters by number
- **Full extraction** - extract entire book as markdown
- **Search** - find text with surrounding context

## Directory Structure

```
~/.claude/skills/epub/
├── SKILL.md                              # Skill definition (triggers on EPUB-related requests)
├── AGENTS.md                             # This documentation
├── CLAUDE.md -> AGENTS.md                # Symlink
└── scripts/epub-reader/
    ├── package.json
    ├── tsconfig.json
    ├── src/index.ts                      # TypeScript source
    └── dist/                             # Compiled JavaScript
```

## Technology Stack

- **TypeScript** - main implementation language
- **jszip** - extract EPUB contents (EPUBs are ZIP archives)
- **xml2js** - parse OPF/NCX metadata files
- **turndown** - convert HTML content to Markdown
- **commander** - CLI argument parsing

## CLI Commands

```bash
# View metadata
node ~/.claude/skills/epub/scripts/epub-reader/dist/index.js metadata "<file.epub>"

# List table of contents
node ~/.claude/skills/epub/scripts/epub-reader/dist/index.js toc "<file.epub>"

# Read specific chapter (1-indexed)
node ~/.claude/skills/epub/scripts/epub-reader/dist/index.js chapter "<file.epub>" <number>

# Extract entire book
node ~/.claude/skills/epub/scripts/epub-reader/dist/index.js full "<file.epub>"

# Search for text
node ~/.claude/skills/epub/scripts/epub-reader/dist/index.js search "<file.epub>" "<query>"
```

## How the Skill Works

1. **SKILL.md** defines when Claude should use this skill (any EPUB-related request)
2. Claude automatically invokes the appropriate CLI command based on user intent
3. Output is clean Markdown suitable for reading and analysis

## Rebuilding

If you need to modify and rebuild:

```bash
cd ~/.claude/skills/epub/scripts/epub-reader
npm install
npm run build
```

Restart Claude Code after any changes to SKILL.md for them to take effect.
