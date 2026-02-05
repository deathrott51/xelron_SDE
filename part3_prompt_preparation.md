# Part 3: Prompt Preparation

## Selected PR
Beets PR #3509 – Unicode Handling in File Paths on Windows

### Repository Context

Beets is a command-line music library manager designed to normalize metadata and organize audio files automatically. It integrates with MusicBrainz to retrieve authoritative metadata and applies user-defined templates to rename and arrange files. The tool targets users who value precision, automation, and control over their music collections.

### Pull Request Description

This pull request resolves a Windows-specific failure caused by inconsistent unicode handling in filesystem operations. Windows internally represents paths using UTF-16, while previous code paths relied on locale-dependent encodings. As a result, operations failed for filenames containing characters outside ASCII.

The fix introduces a consistent internal representation for paths and ensures conversion only occurs at filesystem boundaries. All file operations were updated to use centralized utilities, and plugins were refactored to follow the same approach.

### Acceptance Criteria

- File operations succeed with unicode paths on Windows
- Existing ASCII-only workflows remain unchanged
- Plugins handle unicode paths consistently
- Paths stored in the database remain valid and readable

### Edge Cases

- Mixed-script filenames
- Long Windows paths
- Python 2 and Python 3 string differences
- Network UNC paths
- Varying system locales
