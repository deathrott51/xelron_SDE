# Part 2: Pull Request Analysis

## Repository: beetbox/beets

### PR #3145 – Add Support for original_year

**Link**  
https://github.com/beetbox/beets/pull/3145

#### Summary

This pull request introduces an `original_year` field to distinguish an album’s original release date from the release date of a specific edition or remaster. Previously, Beets stored only a single year value, which often reflected the reissue date rather than the album’s historical release. The change allows users to organize collections based on original release chronology while retaining edition-specific metadata.

#### Technical Changes

- Database schema extended to include `original_year`
- MusicBrainz integration updated to read release-group first-release dates
- Import workflow updated to populate both `year` and `original_year`
- Query syntax and path templates extended
- Database migration and test coverage added

#### Impact

The change is backward-compatible and additive. Existing libraries continue to function without modification, while users gain more accurate chronological organization options.

---

### PR #3509 – Fix Unicode Handling in File Paths on Windows

**Link**  
https://github.com/beetbox/beets/pull/3509

#### Summary

This pull request fixes failures when handling file paths containing non-ASCII characters on Windows. Prior behavior caused encoding errors when processing filenames with characters outside the system code page. The fix ensures consistent unicode handling across all filesystem operations.

#### Technical Changes

- Introduced centralized path conversion utilities
- Updated all filesystem operations to use safe path handling
- Refactored import and plugin workflows to normalize paths early
- Expanded test coverage with multilingual filenames

#### Impact

This change significantly improves reliability for Windows users with international music collections. Existing behavior on Unix-like systems remains unchanged.
