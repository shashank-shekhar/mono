# Multi-Folder Test Structure

This demo-blog has been set up to test the multiple content folders feature.

## Folder Structure

```
demo-blog/
├── blog/                           # Level 1 - Main blog folder
│   ├── 2024/                       # Level 2 - Year folder
│   │   ├── tech/                   # Level 3 - Tech category
│   │   │   ├── ai-trends.md
│   │   │   └── web-performance.md
│   │   └── personal/               # Level 3 - Personal category
│   │       └── work-life-balance.md
│   └── 2023/                       # Level 2 - Archive
│       └── year-review.md
├── tutorials/                      # Level 1 - Tutorials folder
│   ├── web/                        # Level 2 - Web tutorials
│   │   ├── html-basics.md
│   │   └── css-styling.md
│   └── mobile/                     # Level 2 - Mobile tutorials
│       └── flutter-intro.md
├── notes/                          # Level 1 - Notes folder
│   ├── quick-tip-git.md
│   └── reading-list.md
└── posts/                          # Legacy folder (for backward compat testing)
    └── ... (existing demo posts)
```

## Configuration in project.mon

The `project.mon` file includes a comprehensive content folder configuration:

```toml
[[content.folders]]
path = "blog"
title = "Blog"
icon = "📝"

[[content.folders]]
path = "blog/2024"
title = "2024 Posts"

[[content.folders]]
path = "blog/2024/tech"
title = "Tech"

# ... (see project.mon for full config)

[content]
defaultFolder = "blog"
autoDetectNesting = 0
```

## Test Cases Covered

### 1. Multiple Top-Level Folders ✅
- `blog/` - Primary blog content
- `tutorials/` - Tutorial content
- `notes/` - Quick notes
- `posts/` - Legacy backward compatibility

### 2. Nested Folders (3 Levels) ✅
- Level 1: `blog/`
- Level 2: `blog/2024/`
- Level 3: `blog/2024/tech/`

### 3. Folder Metadata ✅
- Titles: Custom display names
- Icons: Emoji icons for folders
- Default folder: `blog` is set as landing page

### 4. Content Distribution
- **4 posts** in `blog/` (nested in 2024/tech, 2024/personal, 2023)
- **3 posts** in `tutorials/` (nested in web, mobile)
- **2 posts** in `notes/`
- **Total: 9 new test posts**

## Expected Navbar Output

When implemented, the navbar should generate:

```
Home | 📝 Blog ▼ | 🎓 Tutorials ▼ | 📔 Notes
         |              |
         ├─ 2024 ▼      ├─ Web Development
         │   ├─ Tech    └─ Mobile Development
         │   └─ Personal
         └─ 2023 Archive
```

## Expected Index Pages

- `/` - Shows posts from `blog/` (default folder)
- `/blog/` - All blog posts
- `/blog/2024/` - 2024 posts
- `/blog/2024/tech/` - Tech posts from 2024
- `/blog/2024/personal/` - Personal posts from 2024
- `/blog/2023/` - 2023 archive
- `/tutorials/` - All tutorials
- `/tutorials/web/` - Web tutorials
- `/tutorials/mobile/` - Mobile tutorials
- `/notes/` - All notes

## Testing Checklist

- [ ] Configuration parsing (read content section from TOML)
- [ ] Post scanning (find posts in all folders)
- [ ] Folder metadata assignment (posts have folder/folderTitle)
- [ ] Navbar generation (auto-generate menu from folders)
- [ ] Index page generation (create index for each folder)
- [ ] Nested navigation (dropdowns for nested folders)
- [ ] Default folder behavior (blog posts on landing page)
- [ ] Backward compatibility (existing posts/ folder still works)

## Sample Posts

### Blog Posts (4)
1. `blog/2024/tech/ai-trends.md` - AI Trends in 2024
2. `blog/2024/tech/web-performance.md` - Optimizing Web Performance
3. `blog/2024/personal/work-life-balance.md` - Finding Work-Life Balance
4. `blog/2023/year-review.md` - 2023 Year in Review

### Tutorials (3)
5. `tutorials/web/html-basics.md` - HTML Basics (series: web-fundamentals)
6. `tutorials/web/css-styling.md` - CSS Styling (series: web-fundamentals)
7. `tutorials/mobile/flutter-intro.md` - Introduction to Flutter

### Notes (2)
8. `notes/quick-tip-git.md` - Git Aliases
9. `notes/reading-list.md` - My Reading List

## Next Implementation Steps

1. **Parse content config** in `configLoader.ts`
2. **Update post scanning** in `buildService.ts` to handle multiple folders
3. **Auto-generate navbar** items from folder hierarchy
4. **Generate folder index pages** for each content folder
5. **Test all functionality** with this demo structure
