# postsnag-connector.md

How to run this skill when the PostSnag connector is connected (its tools are named `facebook_*` and `postsnag_*`).

You already have this skill: do not call `postsnag_use_skill` for it.

## 1. Read the library with the tools; do not ask for an export

When those tools are available, they replace the export. Do not tell the user to open the dashboard, click Export or attach a file. Find what they mean, read its posts, and build the same rows the export would have. Every rule in this skill then applies unchanged: thresholds, floors, honesty footer, pointer line.

- **A profile:** `facebook_list_profiles {search}` finds it; its `_id` is the `profile_id`. Read its posts with `facebook_list_posts {profile_id, sort_by: "createdTime", sort_order: "desc", limit: 100}` and follow `pagination.pages`. `facebook_get_profile {profile_id}` carries `followerCount` and `bio`, which the Markdown export would have.
- **A group:** `facebook_list_groups` (or `facebook_get_group`), then `facebook_list_posts {group_id, …}` with the same paging.
- **Someone the user has not captured** (for example a competitor): `facebook_discover_search {query}`, then `facebook_list_posts {fb_user_id | fb_group_id}`. These come from the shared community pool, so say so in the output header.
- **One post:** `facebook_get_post {post_id}`.

Read the most recent 300 posts at most (three pages) unless the user asks for more, and state the count you read, as the skill already requires for any input.

## 2. Each post as an export row

| Profile export column | Group export column | Post field |
| :- | :- | :- |
| `Posted` | `Posted` | `createdTime` (fall back to `createdAt`) |
| `Type` | `Type` | `postType`; treat `reel` as `video` |
| `Reactions` | `Reactions` | `reactions.total` |
| `Comments` | `Comments` | `commentCount` |
| `Shares` | `Shares` | `shareCount` |
| `Views` | — | `viewCount`, on video and reel rows only; `0` or missing on any other row is absent, not zero |
| `Duration_Sec` | — | `durationSec`; `0` or missing is absent |
| `Content` | `Content` | `content` (may be empty) |
| `Post_URL` | `Post URL` | `postUrl` |
| `Media_URLs` | — | `mediaUrls` |
| `Link_Title`, `Link_URL` | — | `linkPreview.title`, `linkPreview.url` |
| — | `Author`, `Username` | `authorName`, `authorUsername` |

**Timestamps are UTC.** `createdTime` is an ISO instant ending in `Z`. The timezone rule in this skill still applies: before any clock-time advice, ask the user their local timezone and convert. Run the skill's date-only test (most times at midnight) on the converted value as well as on the UTC value, and treat the capture as date-only if either one trips it.

## 3. What the connector adds

- **Visuals:** the skill's visual sections need images the user supplies. Here `facebook_view_media {post_ids}` returns the pictures and still frames from videos, and counts as supplied. Ask only for the posts the section needs, such as the top 10, because images are expensive. Never open `mediaUrls` yourself.
- **Comment text:** the skill says the export has no comment text. The connector has the comments the user opened on Facebook: `facebook_get_comment_threads {profile_id | group_id | post_id}`. Capture is partial, so report the number captured against `commentCount` and never treat it as every comment.
- **Video transcripts:** `facebook_get_post` returns a video's transcript when one was captured.

## 4. Plan limits

The connector is for paid plans, so the 30-post free-tier cap the skill describes does not apply. A small library still runs in lite mode under the skill's own post-count thresholds.
