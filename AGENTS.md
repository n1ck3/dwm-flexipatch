# DWM FlexiPatch Agent Guidelines

## Build Commands
- `./install.sh` - Clean build and install (removes patches.h/config.h, rebuilds, installs, HUPs dwm)
- `make clean && make` - Full rebuild
- `make` - Incremental build  
- `make install` - Install dwm (requires sudo)
- No unit tests - this is a window manager

## Repository Management
- **Fork Strategy**: Fork from bakkeby/dwm-flexipatch upstream
- **Branches**: 
  - `master`: Pristine, exactly matches upstream/master, NEVER alter
  - `prod`: Production changes on top of origin/master (== upstream/master)
  - `test`: Testing branch, always stems from origin/prod
- **Updates**: Sync master with upstream, rebase prod against master, rebase test against prod
- **Upstream**: `git remote add upstream https://github.com/bakkeby/dwm-flexipatch.git`

## Code Style
- **Language**: C99 (`-std=c99`)
- **Indentation**: Tabs (not spaces)
- **Naming**: snake_case for functions/variables, SCREAMING_SNAKE_CASE for macros
- **Headers**: System headers first, then X11, then local headers
- **Patches**: Use preprocessor directives (#if PATCH_NAME) to conditionally include code
- **Config**: Copy config.def.h to config.h and patches.def.h to patches.h before building
- **Error handling**: Check X11 function returns, use die() for fatal errors
- **Memory**: Free allocated memory, especially X resources
- **Style**: K&R style braces, compact code preferred
- **Comments**: Minimal, only when necessary for clarity
- **Functions**: Static by default unless needed externally