# Changes

:warning: After using the latest version, if you wish to open your collection with an
earlier Anki release, please go to the File>Switch Profile menu item, and click
on "Downgrade & Quit". If you skip this step, you may get an error message when
opening your collection in an older Anki version, and you will need to return to
this version, downgrade, then try again.

## Changes in 2.1.45

A [release candidate](https://betas.ankiweb.net) is available.

Undo handling:

- Most actions now support multiple undo steps. You can change a card template,
  delete some notes, bury a card, then undo each of those steps if you wish.
- Actions that support multiple undo steps will now save the changes
  immediately, meaning that if Anki crashes, the changes you made in the last
  few minutes will no longer be lost.
- Most undoable actions can now be redone, so you can undo an accidental undo.
- Actions that don't support the new undo handling (eg, Check Database), will
  clear the undo history.
- Add-ons will clear the undo history if they modify the database directly, or
  use routines that don't support undoing. There are some new routines available
  to add-ons to make operations undoable, but add-ons may need to be updated
  to use them.

Scheduling changes:

- A new scheduler is available, with a number of improvements. Please see the
  [2021 scheduler page](https://faqs.ankiweb.net/the-2021-scheduler.html) for
  more information.
- The deck list now shows the learning count separately.
- On new collections, the v2 scheduler is now the default.

Browser changes, mostly thanks to Rumo:

- The sidebar now has two modes. The default allows clicking on items to search
  for them. The other mode allows you to select multiple items at once, so you
  can drag & drop or delete multiple items.
- The browse screen can now be toggled between showing cards,
  and showing notes.
- When showing notes, some columns will show an aggregate over all the
  cards of a note.
- Added an introduced:x search to locate cards first studied in the last x days.
- Column rendering has been moved into the backend, and will be faster than
  before (but is still limited by the speed of the graphics toolkit).
- A fair bit of the browser code has been changed, and some add-ons like the
  "Advanced Browser" add-on will need to be updated to support the new approach.
- New tag icons and associated backend work (thanks to Henrik).
- Added an option in the Preferences screen to customize the starting
  search text (eg, to start with "deck:current").
- More reliably scroll to the current card.
- When opening the Browse screen with an active study card, the whole
  deck is now shown.
- Added 3 new flag colours.
- Flags can now be renamed in the sidebar.
- Horizontal scrolling in the browse screen is less jumpy.
- Sidebar items can be dragged onto the Saved Searches area to add them as a favourite.

Editor changes, mostly thanks to Henrik:

- A new editor toolbar implementation, with improved icons and handling.
- The editor now provides bullet and numbered list buttons.
- The editor now provides buttons to control text alignment and indent.
- Sticky fields can now be toggled on/off from the editing screen.
- A new API is available for add-ons, and the existing API should continue
  to work.
- The HTML editor is now shown inline, and supports syntax highlighting,
  and showing opening/closing tags.
- Warn user when they attempt to use cloze markers inappropriately
  (thanks to Rumo).

State handling:

- When you make changes, the user interface should update more consistently now.
  Adding a new tag to a note will update the sidebar in the Browse screen for
  example, and when you review a card that is shown there, the columns will
  update.
- The Browse screen no longer refreshes a search automatically. When you make a
  change, the column text may update, but the number of rows will not change.
  Deleted cards show "(deleted)" until you search again.
- The main window no longer shows a "waiting for editing to finish" screen. When
  you make changes such as editing a note, the main window will dim, and will
  automatically refresh when you return to it.

The deck options screen has been reimplemented:

- (Re)learning steps are now shown with units, eg 10m or 4d.
- Deck options are now shown on one scrollable page.
- Extra help is available for most options.
- It is easy to see at a glance which options have been changed from the
  default, and individual options can be reverted to the default setting.
- Warnings will be shown for some common issues (eg, review limit too low
  compared to new cards).
- Some of the more advanced options have been moved to a separate "Advanced"
  section.
- The old options can be accessed with a Shift+click, since it will take a while
  for add-ons to be updated to support the new screen. A new API is available,
  thanks to Henrik.
- The deck description is now accessible via a button in the overview screen,
  instead of via the deck options.

Other features:

- An updated Change Notetype implementation, that can match fields by name, and
  allows you to map a source field to multiple destination fields in order to
  clone a field.
- Pre-load images on answer side (thanks to Hikaru).
- The `[...]` in cloze deletions is now read as "blank" by TTS (thanks to Rumo).
- The Find&Replace option in the Browse screen can now be used on tags as well.
- Added a Card Info option to the review screen.
- When opening deck option from the study screen, you'll now be asked which deck
  you want if the card is in a subdeck.
- You can now choose which add-ons you want to update (thanks to BlueGreenMagick).
- Support system SSL certs on Linux.
- Extra checks are now done when updating a card template, such as detecting when
  a cloze notetype is missing a cloze directive, or two templates have identical question sides (thanks to Rumo).
- Support Ctrl+Numpad Enter to add cards.
- Added night mode styling to 'type in the answer' box, and improve legibility
  of comparison.
- Sidebar search now scrolls to first match (thanks to Abdo & Rumo).

Fixes:

- Custom study now limits the tag selection to 100 tags or fewer, to prevent errors caused by exceeding database limits.
- Fixed an issue compiling on recent Python 3.9 installs.
- Fixed audio getting stuck when pausing near end (thanks to kelciour).
- Fixed building on linux-arm64 (thanks to qubist-pixel-ux).
- Fixed Card Info screen not ignoring manual rescheduling when calculating the average time.
- Fixed crash when pressing the copy shortcut with no active selection.
- Fixed current review card sometimes changing when making edits.
- Fixed deck options tooltip appearance (thanks to Matthias).
- Fixed escaping of hyphens in searches (thanks to Rumo).
- Fixed field pin status being forgotten when opening Cards screen (thanks to Henrik).
- Fixed incorrect card count when removing multiple templates.
- Fixed incorrect font on Windows (thanks to Kelciour).
- Fixed resource leak in sound code (thanks to Kelciour).
- Fixed some instances of a flash when revealing answer on cards with images.
- Fixed text with single quote not being escaped in export (thanks to Ryan).
- Fixed various links to the manual (thanks to cherryblossom000).
- Force x11 mode when the packaged build is run on a system that tells Qt to use
  Wayland, as Wayland is not currently supported by the packaged build.
- Numerous behind-the-scenes improvements from Henrik and Rumo.
- Other fixes and improvements, thanks to Abdo, Glutanimate, Arthur, Shaun,
  hkr and others.
- Performance improvements and other miscellaneous fixes.

## Changes in 2.1.44

Released 2021-05-04.

- Search text is no longer automatically quoted/interspersed with ANDs.
- Fix two backslashes being treated as one in MathJax.

## Changes in 2.1.43

Released 2021-04-03.

- The reviewing screen will now wait for up to 100ms
  for images to load before showing, and waits until images
  have been loaded before scrolling to the answer.
- The default fade-in on the review screen has been removed.
- Fix DB check incorrectly identifying an issue after
  lapsing a card with a non-zero interval % in the V1 scheduler.
- Fix editing toolbar being initially active (thanks to Henrik).
- Fix some error messages (thanks to Rumo).
- Fix expand/collapse triggering click in sidebar (thanks to BlueGreenMagick).
- Update translations, thanks to the translators.
- Fix "Forgot Card" message.
- Fix deck list not updating after deleting.

## Changes in 2.1.42

Released 2021-03-10.

- Fix sync downloads failing when temp folder on separate partition.
- Fix RTL fields (thanks to Abdo).
- Fix issues with field focusing and caret positioning (thanks to Henrik).
- Strip comments when pasting HTML (thanks to Abdo).
- Don't forget CSV delimeter when canceling dialog (thanks to Benjamin).
- Fix stale caches after rolling back to a checkpoint (thanks to Rumo).

For build hashes, please see the [GitHub releases
page](https://github.com/ankitects/anki/releases).

## Changes in 2.1.41

Released 2021-03-07, build 312fa278.

Browser improvements:

- Tags now show in a tree (thanks to Abdo).
- Added a search bar to the sidebar (thanks to Abdo).
- New context menu actions to rename or remove tags and their children, rename
  decks, manage notetypes, and rename/remove saved searches (thanks to Abdo
  and BlueGreenMagick).
- The preview button in the browse screen has moved into the editing area (thanks to Henrik).
- With the improved sidebar, a number of options have been removed from the Filter button.
- The remaining items in the Filter button have been moved into the sidebar, and
  the Filter button removed.
- Tags and decks can now be dragged and dropped in the sidebar.
- Each section can now be expanded/collapsed.
- "Due" now shows only cards due that day.
- Added "Overdue" item.
- Click on Decks to show whole collection.
- Click on Flags to show any flag.
- Click on Tags to show all non-empty tags.
- Added "Untagged" under Tags.

Editing improvements:

- `<br>` tags will now be used by default instead of the previous `<div>`
  tags, which solves some issues with multiple lines in cloze deletions and
  MathJax (thanks to Henrik).
- The tags field in the editor now autocompletes from anywhere in a tag name,
  not only the start.
- Invalid field content can no longer spill out into the editing area (thanks to Henrik).

Search improvements:

- Searches are now rewritten into a canonical format (eg `one two` becomes
  `"one" AND "two"`) (thanks to Rumo).
- Search error messages are now much more specific (thanks to Rumo).
- is:learn, is:due and prop:due now handle more cases, such as suspended cards
  (thanks to Henrik).
- Added prop:pos search to search for new card position (thanks to Abdo).
- Added a shortcut to replace part of a search with a different search
  (eg changing the selected deck) (thanks to Rumo).
- Support resched:x for searching for cards that were manually rescheduled
  in x days (thanks to Henrik).
- Support prop:rated/resched to search for rated/rescheduled cards over
  specific time periods (thanks to Henrik).
- Filtered decks can now be created from a browser search, and vice versa (thanks to Rumo).
- Filtered deck screen now has a link to show cards not matched by search (thanks to Rumo, Abdo).
- Better ergonomics for developers (thanks to Rumo).

Graph improvements:

- A number of the graphs can now be clicked on to search for the cards
  displayed by the graph (thanks to Henrik).
- The starting day of week can now be altered in the Calendar graph (thanks to Henrik).
- The Card Counts graph now supports toggling separate suspended/buried counts (thanks to Henrik).
- The intervals and ease graphs now covers more cases, such as suspended cards
  (thanks to Henrik).
- Place less emphasis on outliers in the Calendar graph (thanks to Henrik).
- Ignore manually scheduled cards in hour graph.

Scheduler improvements:

- The V2 scheduler no longer applies parent review limits to child decks.
  Previously the limits were inconsistently applied, which could lead to the
  deck list not reflecting the actual number of cards you'd receive when you
  clicked on a deck. AnkiMobile and AnkiWeb have been updated to match this
  behaviour, and AnkiDroid will also be updated soon. Using 2.1.41 in
  conjunction with older clients will not cause any problems when syncing, but
  you may find the deck list/review counts do not match.
- The V1->V2 upgrade process no longer resets cards that are in learning, or
  removes cards from filtered decks.
- Users on the old scheduler will now see a message at the top of the deck
  list prompting them to update to the Anki 2.1 scheduler.
- There is no option to downgrade to the V1 scheduler anymore, though you can
  still do so by downgrading to an older Anki version first.

Reworked the Reschedule tool:

- Split into separate "Forget" and "Set Due Date" actions
- "Set Due Date" defaults to not adjusting the card interval.
- Changed the "Delete Tags" shortcut; Ctrl+Shift+D now changes the due date.
- Added the action to the review screen as well.
- Input now remembered.

Other changes:

- A basic sync server is now built into Anki. It does not yet support
  media. Docs are in the docs/ folder of the source tree.
- The title bar on Macs will now turn dark when night mode is activated.
- Deck descriptions of the congratulations screen can be enabled by turning markdown
  on in the deck options, but only 2.1.41+ will be able to render the markdown.
- Add opus to media list in editor.
- Edit/More buttons auto-hide when window is small (thanks to Henrik).
- Support Alt+number to switch between clozes in the card layout screen (thanks to Abdo).
- Use monospace font in HTML editor.
- Improve error message when trying to nest under a filtered deck (thanks to Rumo).
- Reposition dialog's "shift cards" option now defaults to off.
- Other fixes and improvements thanks to Henrik, Rumo, Abdo, Arthur, Maksim, Guillem,
  stayingpeachy, Daniel, khonkhortisan and Kerrick.

Fixes:

- Fix the Reposition command not preserving the browser sort order.
- Fix some issues causing the sync indicator to show unnecessarily (thanks to Rumo).
- Fix slowdown after large "check media" report.
- Fix a spurious warning about a full sync when renaming card templates.
- Fix a freeze when answering a card with a missing parent deck.
- Fix Anki not working after installing on Linux over a previous install.
- Don't log card resets when exporting.
- Fix congrats screen not showing when learning cards were due soon.
- Updated bundled lame and mpv on Windows and Mac builds.

For developers:

- Add-on authors, please see
  <https://forums.ankiweb.net/t/add-on-porting-notes-for-anki-2-1-41/7390>
- Almost all of the Python codebase now has type hints. 🎉
- JS libraries like jQuery have been updated (thanks to Henrik).
- Add (untested) support for ARM64 Linux.
- orjson is turned back into an optional requirement (though is still
  recommended, as it's faster).
- The sidebar code has been moved from from browser.py into sidebar.py, which
  may break some add-ons.

## Changes in 2.1.40

Released 2021-02-07, build cf446733.

- Fixed backup not being made when choosing "Download" when syncing.
- Fixed a slowdown after importing.

## Changes in 2.1.39

Released 2021-02-02, build 576f0043.

- Fix the Reposition command not preserving the browser sort order.
- Fix some issues causing the sync indicator to show unnecessarily (thanks to Rumo).
- Fix a spurious warning about a full sync when renaming card templates.
- Fix Anki not working after installing on Linux over a previous install.
- Don't log card resets when exporting.
- Fix congrats screen not showing when learning cards were due soon.
- Updated bundled lame and mpv on Windows and Mac builds.
- Other fixes and improvements, with thanks to Henrik, Rumo, Abdo, Arthur, Guillem, Meredith, Gustavo, and Daniel.

## Changes in 2.1.38

Released 2020-12-26, build 355e4cd5.

- Use a new approach for recording audio. If you encounter any issues,
  the old PyAudio driver can be selected in the Preferences screen. The old
  driver will likely be retired in the future, so please let us know
  if the default system does not work for you.
- All built-in Windows TTS voices should now be supported on recent Windows 10
  releases (thanks to Ryan).
- Fix the Reposition tool in the Browse screen not following the sort
  order.
- Reduce the default fade time in the review screen.
- The ANGLE video driver can now be selected in the Preferences on Windows.
- Fix some instances of the sync indicator remaining on after sync (thanks to Rumo).
- Work around --text-fg appearing in fields.
- Fix link in about screen (thanks to Abdo).
- Fix '1' being shown instead of the correct number in some Russian translations.
- Fixed invisible characters when adding new card templates (thanks to Henrik).
- Fixed duplicate check getting confused by non-breaking spaces (thanks to abdo).
- Don't throw error when computer hostname is invalid.
- Other minor changes (thanks to Henrik & k12sh)

For developers:

- Protobuf binaries are now used to speed up the initial build.
- Fixed Python code completion, and added some info to docs/development.md
- ./run now runs Anki with Python warnings enabled - PRs that fix any that come
  up would be welcome (thanks cecini for the first!)

## Changes in 2.1.37

Released 2020-12-12, build 6d596c8f.

- Fixed filtered decks not honoring sort order.
- Fixed review screen not automatically scrolling to answer (thanks to Henrik).
- The deck options screen now limits minimum ease to 131%.

For developers:

- Added a scripts/build command to build the redistributable wheels.
- The Rust worker is disabled by default, as some users had trouble building with it.

## Changes in 2.1.36

Released 2020-12-09, build c505894b.

Notable changes:

- Alternate builds have been discontinued. If you are using a 32 bit system, or
  a macOS version older than 10.13, Anki 2.1.35 is the last release you will be able
  to update to.
- MathJax has been updated to version 3, thanks to Henrik. It should render faster
  than before. If you were customizing the MathJax configuration using Javascript,
  you will need to
  [use a new method](https://github.com/ankitects/anki/pull/809#issuecomment-721438738).
- A separate mpv process is now used to play videos on Windows, which should
  solve issues with playing getting stuck, thanks to Kelciour.
- The handling of wildcards and escape characters in search [has been
  reworked](https://docs.ankiweb.net/#/searching?id=matching-special-characters)
  to be more consistent, thanks to Rumo.
- Early startup messages are now translable, thanks to Abdo.
- When cards are rescheduled in the browse screen, a review entry log is now created.
- The main card area is now focused instead of the bottom area during review,
  which allows using the keyboard to scroll, thanks to Henrik.

Bugfixes:

- Fixed corrupt indexes when checking database.
- Fixed duplicate search when sort field is not first field (thanks to Abdo).
- Fixed error when switching to note type with fewer fields.
- Fixed invalid utf8 in notes when checking database.
- Fixed invisible scrollbar in night mode + browser.
- Fixed issues with "find duplicates" (thanks to Abdo)
- Fixed some issues with adding/renaming decks (thanks to Cecini).
- Other minor fixes.

For developers:

- Anki is now built using Bazel. This leads to more reliable builds, and reduces
  the number of dependencies you need to manually install. Please see docs/ for
  updated build instructions, and report any issues you encounter on the user
  forums.
- The minimum Python version has been updated to 3.8.
- The wheels available on PyPI support both Python 3.8 and 3.9.
- All translations have been migrated to [Fluent](https://translating.ankiweb.net/#/anki/developers).
- Normal and night mode theming now uses CSS variables, making it easier to override in add-ons.
- The congrats screen, burying/suspending, filtered deck building/emptying, browser sidebar, and card
  reposition/reset have been reworked. If you were modifying them in an add-on, your add-on
  may need updating. For the congratulations screen, see the new webview_did_inject_style_into_page
  hook

Thanks to all the people who have contributed bugfixes and code/doc updates:
Abdo, Lukkea, Akshara, Kelciour, David, Henrik, Colin, Johan, Piotr, Andreas,
Arthur, Alan, RumovZ, Cecini, Soren, Krish, ianki, Cyphar and kaczmarj, in no
particular order.

Thanks also to all of the people who have contributed translations for this
and previous releases: <https://i18n.ankiweb.net/contributors/>

## Changes in 2.1.35

Released 2020-10-02, build 84dcaa86.

- Fix a bug in Anki 2.1.29+ that caused excessive memory and CPU usage
  on long-running operations that show a progress bar, such as importing.
- Roll back Mac and Windows builds to Qt 5.14 again,
  as there are still issues with 5.15.
- Fix display issue in graphs on alternate Mac build.
- Fix preview not updating on multiple selection (thanks to abdo).
- Fix old content appearing when flagging immediately
  after typing.
- Fix some handling of `*` in searches.
- Sidebar now correctly escapes some characters (thanks to abdo).

## Changes in 2.1.34

Released 2020-09-24, build 8af8f565.

- Fix a bug in Anki 2.1.28+ where a newly created deck config would default to
  an ease of 130%. When updating, Anki will automatically change any deck
  configs with an ease of 130% back to 250%, and change any cards using those
  deck configs with a low ease back to an ease of 250%. Users who updated from
  an older Anki version and did not add new deck configurations should not be
  affected. If you have deliberately set an initial ease of 130%, please change
  it to 131% or greater prior to upgrading, so that Anki leaves your settings
  alone. Thanks to Aleksa for discovering the issue.
- Update the standard builds to the latest GUI toolkit version.
  Please report any improvements or regressions you notice.
- Dropped audio plays automatically again (thanks to abdo).
- Revert to older sound playing behaviour to work around issues
  (thanks to kelciour).
- is:due now stops at now+learn ahead limit, instead of end of day.
- Various improvements/fixes, some thanks Aleksa & Henrik.

## Changes in 2.1.33

Released 2020-08-30, build 3f403040.

- Access More button in review screen with 'm' (thanks to ANH).
- Audio no longer plays when dropped/pasted (thanks to ANH).
- Fix bulk tag adding not adding tags if tag is a substring of an existing tag (thanks to Soren)
- Fix cards not being unburied if leaving Anki open and the first action of a new day is a sync.
- Fix drag&drop into existing content (thanks to ANH).
- Fix error when add-ons tried to access note/template in card template screen.
- Fix next learn message in congrats screen.
- Fix nonbreaking spaces in filenames not being handled properly.
- Fix text in export file selector (thanks to ANH).
- Fix timeouts in full syncs and media syncs again.

## Changes in 2.1.32

Released 2020-08-25, build dee7d45d.

- Roll back a change in the previous update that could cause syncs to time out.
- Fix sign up link in login screen.

## Changes in 2.1.31

Released 2020-08-23, build 13476503.

- Show card counts in pie graph, and other minor graph tweaks.
- Fix sync error+lost review when undoing in v2 filtered deck with scheduling off.
- Fix crash when dragging & dropping, thanks to ANH25.
- Fix 'stale notetype' error after sync+add.
- Close "edit current" when current card deleted.
- Code improvements thanks to ANH, Arthur, Evandro, Henrik and Thomas.
- Find&Replace completion is now case sensitive.
- Fix crash when recovering notes with missing notetype.
- Fix duplicate detection when input text is not normalized.
- Fix Empty Cards not ignoring BR tags.
- Fix Find&Replace window sizing.
- Fix handling of nested legacy template directives.
- Fix issues with bulk tag removal.
- Fix mpv failing to play audio after it's restarted, thanks to Kelciour.
- Fix some (rare) crashes.
- Full syncs and media syncs now terminate more quickly when the connection breaks.
- Improve support for getting proxies from Windows registry.
- Remove embedded direction markers in RTL cloze deletions.
- Strip nul characters from tags.

## Changes in 2.1.30

Released 2020-08-09, build 06a69c25.

- Work around a failure to start on some Windows 10 May 2020 installations.
- Fix "show windows in tabs" not working on standard macOS build.
- Fix move into/out of filtered decks not syncing.
- Add right axis to graphs.
- Add night mode and mobile class toggles in card layout screen (thanks to ANH25).
- Card counts graph now always shows table.
- Catch negative review times in DB check.
- Code improvements (thanks to Matt, phwoo, Evandro and aplaice).
- Fix a crash in the DB check when a note type was missing.
- Fix automatic logout not working when auth failure occurs.
- Fix deck list and graphs not including v2 scheduler cards with rescheduling disabled.
- Fix early reviews not appearing in review graph.
- Fix hour graph problem in timezones west of UTC.
- Fix negated conditonals being non-negated when renamed.
- Fix some syncing errors that could happen until Check Database was run.
- Fix some young cards being shown as mature in reviews graph.
- Handle multiple same-numbered clozes in cloze-only filter.
- Refresh tag list after clearing empty tags.
- Other minor fixes.

## Changes in 2.1.29

Released 2020-07-28, build bbff62bf.

- Add cloze-only: template filter, which can be combined with TTS to speak only the elided part.
- Fixed AltGr key handling in standard Windows build.
- Fix some Windows performance problems by rolling back to an older
  Qt version.
- Support the terminal command that enables dark mode on macOS again.
- Start media sync after full sync finishes.
- Fixed mpv taking time to start (thanks to Kelciour)
- Code/build improvements (thanks to Evandro, Matt & Arthur).
- Use right-to-left direction in some webviews when using RTL interface language.
- Fixed card ID and note ID being flipped in card stats.
- Don't show an error when card contains an empty URL.
- Various fixes for deck statistics.
- Fixed preview not updating when editing text in the Browse screen.
- Close gracefully on SIGTERM.
- Other minor tweaks.

## Changes in 2.1.28

Released 2020-07-20, build 7d8818f8.

2.1.28 is a big update with changes in a number of areas.

- A reworked graphs screen:

  - Rewritten with new graphing tools for more interactivity.
  - Graphs can now be displayed for arbitrary searches.
  - Added a calendar/heatmap view.
  - If you need them for add-ons, the old graphs are currently still
    accessible with a shift+click on the Stats button.

- Reworked syncing:

  - Normal syncs and media syncs can operate in parallel, speeding up startup and shutdown.
  - Normal syncs no longer need to close open windows like the Browse screen, or close & re-open
    the collection.
  - Full syncs now show a progress bar.
  - Full syncs can now be cancelled, and both normal and full syncs cancel more quickly.

- Card generation changes:

  - Card generation now supports negated conditionals, and a mix of required
    and optional fields.
  - When adding/importing, if a normal note doesn't generate any cards, Anki
    will now add a blank card 1 instead of refusing to add the note.
  - Please bear in mind that if you take advantage of these features, older Anki
    clients may report the cards are blank, or try to clean them up when you
    use the Empty Cards feature.
  - Cloze numbers over 499 are no longer supported.

- Card template screen:

  - Changes are now accumulated, and can be saved or discarded when you close the screen.
  - The front, back, and styling are no longer shown at the same time. You can switch between them with ctrl+1/2/3 or cmd+1/2/3.
  - Added a search bar to search for text in the template or styling.
  - Added a dropdown to change the previewed cloze number.
  - Added a checkbox to toggle the filling of empty fields for preview.
  - You can now delete a card template even if some notes are only using that
    template - they will be given a blank card 1 instead.

- Scheduling:

  - The deck list no longer caps counts to 1000.
  - The overview and study screen no longer cap counts to 1000.
  - The deck list will no longer show a parent count higher than the limit
    set on the parent.

- Empty cards screen:

  - Notes will not be deleted by default.
  - Empty cards are grouped by note type.
  - Empty cards can be clicked on to reveal them in the browse screen.

- Database check:

  - Notes with the wrong field count are now recovered instead of being deleted.
  - Notes with missing note types are now recovered instead of being deleted.
  - Notes with missing cards are now recovered instead of being deleted.

- Unicode normalization:

  If you are studying rare CJK characters and wish to prevent them from being converted into
  modern equivalents, the following in the debug console will stop Anki from normalizing note text.

  ```py
  mw.col.conf["normalize_note_text"] = False
  ```

- The standard Windows build has troubles with the AltGr key. This is fixed
  in the 2.1.29 beta, or [a workaround is available](https://forums.ankiweb.net/t/altgr-shortcuts/67).

- The standard Mac build currently does not support native dark mode. If you
  previously enabled it from the terminal, please either try the 2.1.29 beta, or
  undo the change with the following terminal command:

  ```py
  defaults write net.ankiweb.dtop NSRequiresAquaSystemAppearance -bool yes
  ```

Other changes:

- Performance improvements to a number of screens.
- Fields screen now accumulates changes, which can be saved or discarded when you close the screen.
- Updated a few screens to show progress bars instead of hanging the UI.
- The standard builds now use Qt 5.15.
- Audio player on Windows has been switched back to mpv. Please report any
  issues you have playing audio files/videos.
- Fixed is:review not including relearning cards.
- Scroll media log to bottom at start (thanks to Kelciour)
- Update local media server (thanks to Evandro).
- Use Qt colour picker on Linux (thanks to Andreas).
- Add edited:x search for matching notes edited in last x days.
- Improvements to mpv handling (thanks to Kelciour).
- Windows build fix (thanks to Evandro).
- Clearer error message on failed regex search.
- Find & Replace remembers input (thanks to Evandro).
- Code improvements (thanks to BlueGreenMagick, Thomas and Andrew).
- Fixed '&' being changed in image filenames in HTML editor.
- Fixed exports getting broken by Windows carriage returns in note fields.
- Fixed deck deletion, and allow "deleting" the default deck (it comes back empty).
- Card layout screen divider can now be adjusted (thanks to Evandro).
- Fixed duplicate rendering in card layout screen (thanks to Evandro).
- Fixed off-by-one in field drag&drop (thanks to BlueGreenMagick)
- Various other fixes, including contributions from BlueGreenMagick, Arthur, neitrinoweb
  and kenden.

## Changes in 2.1.27

This number was reserved for a bugfix release.

## Changes in 2.1.26

Released 2020-05-09, build 70784154.

- Fixed saving of searches in the browse screen.
- Fixed card layout screen failing to open in the alternate Anki build.
- Fixed .log files appearing when exporting.
- Fixed an error appearing when undoing V2 filtered decks with scheduling disabled.
- Fixed duplicate search when text contains formatting.
- Improvements to the PyPI packages (thanks to Evandro).
- Tweak the handling of changed note types in the add screen (thanks to Arthur).
- Tolerate decks with missing modification time from third party software.
- Support SOCKS proxies in the non-media sync.

## Changes in 2.1.25

Released 2020-05-01, build 898801eb (PyPi 6046bbc7)

- Fix a change to deck configurations that was breaking AnkiDroid.
- Fix deck configurations not deleting.
- Fix angle brackets inside cloze+MathJax not working properly.
- The DB check fixes an AnkiMobile bug where tags were not searchable.
- Revert to an earlier macOS toolchain to work around recordings not working.
- The media check no longer fails when files with very long filenames are in the folder.
- More gracefully handle case where deck conf is missing.
- Don't throw an error when cards have an invalid due number.
- {{type::Field}} now marks the card as non-empty if Field is non-empty.
- Tweak tab width in card layout screen (thanks to BlueGreenMagick).
- Build fixes (thanks to Evandro).

## Changes in 2.1.24

Released 2020-04-28, build 359b9f5c.

Searching:

- You can use `w:something` to search on word boundaries, eg:
  - `w:dog`  
    search for "dog" on a word boundary - will match "dog", but not "doggy"
    or "underdog".
  - `w:dog*`  
    will match "dog" and "doggy", but not "underdog".
  - `w:*dog`  
    will match "dog" and "underdog", but not "doggy".
- You can now use `re:something` to search via regular expression, eg:
  - `"re:(some|another).*thing"`  
    find notes that have "some" or "another" on them, followed by 0 or more characters, and then "thing"
  - `re:\d{3}`  
    find notes that have 3 digits in a row
  - When searching by regex, unicode case folding is used, so searching for `re:über` will
    show a card that has "Über" on it.
- `nc:something` (short for "no combining (characters)") can be used to search while
  ignoring accents, eg `nc:uber` will match both "über" and "Über". This behaves the same way as the "Ignore Accents" add-on, but is about 16x faster.
- You can now sort on the deck, card template, note type and tags columns.
- You can now use wildcards when limiting the search to a field, eg `field*:something`.
- You can now use wildcards when searching for a card template or note type by name.
- `rated:x` searches are now capped to a year instead of a month.
- You can now escaped double-quotes in a search - eg `"foo\"bar"`
- Single-quote searches are no longer supported.
- Because the searching code has been rewritten, add-ons that modify the search
  code will need to be updated to support 2.1.24. It is no longer possible to
  override the Finder class - add-ons will need to use the new hooks in the
  browser screen to either rewrite the search text, or perform their own lookups
  instead. The Advanced Browser add-on has already been updated, and can be used
  as an example of how to accomplish things in 2.1.24.
- Non-wildcard searches now do full unicode case folding (eg 'tag:masse' matches 'Maße').
- Wildcard searches do simple unicode case folding.
- The tag list in the Browse screen now uses unicode case folding.

macOS dark mode handling:

- Anki now solely relies on the night mode setting in the preferences to decide
  whether to show in light or dark mode. Some users wanted to run Anki in light
  mode while keeping the rest of their system dark, and there were various
  display problems when dark mode was changed after Anki started that couldn't
  be easily worked around.
- Users who only use dark mode, and preferred the native look of widgets in dark
  mode, can achieve the previous appearance by running the following command in
  the terminal:

  :warning: This will only work if your system is permanently in dark mode!
  If you switch between dark and light mode, the interface will render incorrectly.

  ```shell
  defaults write net.ankiweb.dtop NSRequiresAquaSystemAppearance -bool no
  ```

  And the following in the debug console:

  ```py
  mw.pm.meta["dark_mode_widgets"] = True
  ```

Database changes (mainly of interest to add-on developers):

- Anki now uses Rust's sqlite libraries instead of Python's.
- The 'db' object on the collection retains most of the same API as before, minimizing the amount of immediate code changes that are required.
- Custom sql functions are no longer supported, and named DB arguments (eg "where id = :id") are deprecated.
- The old database code remains in db.py, and add-ons can continue to use it for accessing
  their own databases.
- The database is now behind a mutex, and can be safely accessed from a background thread.
- Various screens like the database check have been updated to run on a background thread,
  so they no longer lock up the UI while they're running.
- The database progress handler has been removed. Anki previous had sqlite call back into
  Python periodically during long-running DB operations so it could drain the UI queue,
  but this would vary in choppyness depending on the type of DB operation being performed,
  and it was the cause of some crashes in the past. Add-ons that perform long-running operations
  should instead use mw.taskman.run_in_background() or their own threading solution moving forward.

Other changes:

- A tweak which should fix some broken add-ons from preventing the collection from being loaded.
- Add socks support to media sync.
- Allow dragging fields to change their position (thanks to BlueGreenMagick).
- Allow selecting add-on config help text (thanks to ijgnd).
- Allow the type answer arrow to be styled (thanks to Evandro).
- Anki will now wait for a media sync to complete or be aborted before closing the collection.
- Build improvements (thanks to Evandro).
- Changed the way cloze deletions in RTL fields are handled, which should address some corner cases.
- Clean up the previewing code (thanks to Arthur). Add-ons that modify the preview screen will need updating.
- Don't force a full sync when DB check finds cards with a high due number.
- Don't show a popup when a network error occurs while syncing media.
- Fixed a case where decks could be sorted incorrectly (thanks to Arthur).
- Fixed a useless log file being created when exporting.
- Fixed add-ons with multiple branches not updating properly.
- Fixed an error that could occur when performing an operation in the browse screen then immediately closing it.
- Fixed Anki closing after a full sync on collection load.
- Fixed current card sometimes not being centered when searching.
- Fixed deck_browser_did_render hook.
- Fixed editor buttons not being highlighted (thanks to Simone).
- Fixed interface getting stuck when a corrupt collection was encountered.
- Fixed media sync waiting forever when connection dropped.
- Fixed progress dialogs failing to appear in a timely manner.
- Fixed tag searches in custom study (thanks to zjosua).
- Fixed the collection_did_load add-on hook.
- Fixed the wrong language shown in the preferences screen for some languages.
- GitHub now checks Windows and Mac builds as well (thanks to Evandro).
- Handle renamed cloze fields when previewing (thanks to BlueGreenMagick).
- Ignore .DS_Store files in the media trash folder.
- Improved invalid HTML/JS error messages (thanks to Evandro).
- Improved the handling of deck deletions (thanks to Arthur).
- Improvements to debug console (thanks to BlueGreenMagick).
- Left-align tags in the browser.
- Media syncs no longer take time to abort.
- More hooks (thanks to Arthur).
- Moved the scheduling options in the preferences to a separate tab, so options fit on the screen even on devices with small screens.
- Prepare for uploading releases to PyPI (thanks to Evandro).
- The media check will now fix file references in fields that broke because a filename was shortened as part of a sync.
- Updated config handling. While there should be no immediate breakages, if you're an add-on author and
  store lists or dicts in Anki's config, please see 676f4e74a.

## Changes in 2.1.23

Released 2020-03-19, build de9543ff.

A macOS-only build that fixes a problem syncing media files
with non-Latin filenames added by previous Anki versions on macOS.

Please see 2.1.22 below for the bulk of the changes.

## Changes in 2.1.22

Released 2020-03-18, build 0ecc189a.

Media syncing improvements:

- Media syncing now happens in the background, so you can continue using
  Anki while the media sync completes.
- Aside from syncing at open and close, Anki will sync any media changes
  every 15-20 minutes.
- You can click on the sync button while the spinner is active to monitor
  progress.
- Long filenames and problematic characters should be handled smoothly now,
  instead of causing syncing errors.
- Anki should no longer sometimes forget to download files when a media
  sync fails due to network errors.
- When media files are added within Anki, Anki now marks them
  in the database immediately, which can make things faster for people with
  slower disks if they are not modifying the media folder externally.

Media check improvements:

- The Check Media function now shows progress, and can be interrupted.
- There is now a separate button to generate missing LaTeX.
- If LaTeX fails to build, the problem card will be revealed in the browse
  screen.
- When Anki finds files that are too long or would cause errors on some
  operating systems, it will automatically rename them and update your notes
  to point to the new filename.

Both media sync and the media check now place deleted files in a media.trash
folder inside your profile, instead of placing the files in the system trash.
You can use the Check Media function to either empty the trash, or restore
the deleted files back to your media folder.

Other changes:

- You can now export .apkg files with the V2 scheduler enabled.
- Add "New #" prefix to the due column for new cards.
- Fixed audio getting stuck on Windows.
- Clear the audio queue when moving between cards with autoplay off.
- Fixed play icons not appearing in browser preview when autoplay off.
- Show next learning card due time, and count for today.
- Restored grey styling of zeros in the deck list that got lost in the night mode changes.
- Improvements to the readability of the scheduling code (thanks to Arthur)
- Add-on hook improvements, thanks to Glutanimate and Arthur.
- Fixed fields containing a filename with non-Latin text from being corrupted when editing HTML (thanks to Evandro).
- Support for validating add-on config schemas (thanks to Arthur).
- Removed the 'too many decks' message in the deck list screen.
- Fix for issue playing audio from flash drive.
- Fixed Anki getting stuck when importing an invalid file.
- More type hints in the code (thanks to Alan).
- Improvements to the build process and building on Windows (thanks to Evandro).
- Support '/' separator in add-on web paths on Windows (thanks to BlueGreenMagick)
- Fix tags that are in the wrong encoding as part of the DB check.
- Hide the default deck in more cases (thanks to Arthur).
- Updates to the translation infrastructure, including tweaks to the way
  the answer buttons and the review history screen show intervals.

## Changes in 2.1.21

Released 2020-03-09, build f1734a47.

- Fixed error messages when playing audio.
- Fixed legacy add-on filters not working (reading generation in Japanese Support, etc).
- The alternate Mac build works properly when macOS is in dark mode now,
  and can be used if you prefer light Anki in macOS dark mode.
- Prevent UI scale from being decreased below 100%, which caused display problems.
- Fixed Anki failing to start on some Windows 7 machines that were missing TTS support.
- Display a more useful message when mpv/mplayer not installed.
- Don't allow exporting into Anki folder.
- Fixed display of AnkiMobile drawings in night mode.
- Fixed interrupting of current audio when autoplay is turned off.
- Night mode defaults to dark grey instead of black card background.
- Fixed {{Deck}} showing filtered deck instead of original deck.
- Fixed an error that could occur with very small learning steps.
- Fixed a negative version number being shown when add-ons incompatible.
- Fixed some invalid HTML in the review screen (thanks to BlueGreenMagic)
- Added back missing fcntl module.

## Changes in 2.1.20

Released 2020-02-14, build 47a1bf8b.

Template changes:

The way Anki combines your card templates and fields has been updated.
Many users will not notice a difference, but if you encounter error
messages inside the review screen and opening and closing the Cards
screen from the editing area does not resolve the issue, please see
[this support
page](https://anki.tenderapp.com/kb/problems/card-template-has-a-problem).

Add-ons that alter the way cards are shown may [need to be
updated](https://anki.tenderapp.com/discussions/beta-testing/1706-anki-2120-updates-to-card-template-rendering).

Audio changes:

- Text to speech is now [supported in card
  templates](https://apps.ankiweb.net/docs/manual.html#text-to-speech).

- Audio buttons are now shown on the card, and can be turned off in
  the preferences. They will show for both regular audio and text to
  speech.

- You can [customize the size and
  colour](https://apps.ankiweb.net/docs/manual.html#audio-replay-buttons).

- Added shortcut keys in the review screen to pause and jump
  forward/backward 5 seconds.

- Anki now starts a new copy of mplayer for each audio file on
  Windows, which avoids the need to create temporary files.

- Added an option in the preferences to not interrupt the currently
  playing audio when answering.

- Fix multiple spaces in filenames from getting truncated when pasting
  sound files.

Night mode:

- The night mode option in the preferences screen now turns the
  interface dark as well.

- On macOS, when the system is in dark mode, Anki will switch to night
  mode automatically.

- Invert LaTeX in night mode (thanks to zjosua).

- Some of the colours in areas like the graphs could be improved -
  pull requests with included screenshots of the changes would be
  appreciated.

Add-on changes:

- Anki will now check for add-on updates automatically once a day.

- Disabled add-ons are now included in the check as well.

- Add-on authors can specify the minimum and maximum Anki version they
  support, and add-ons will be automatically disabled when running on
  an unsupported Anki version.

- Add-on authors can now upload different add-on versions for
  different Anki versions, and Anki will download the correct one.

- A new hook system for add-ons - please see
  [here](https://anki.tenderapp.com/discussions/beta-testing/1704-anki-2120-updates-to-the-hook-system).

- For add-on authors, some more examples using the new hook system are
  available on the following page, including ported versions of the
  clickable tags and additional card fields add-ons:
  <https://github.com/ankitects/anki-addons/tree/master/demos>

Other changes:

- Added the ability to export selected notes from the Browse screen
  (thanks to Arthur).

- Updated to a newer toolkit.

- Emptying a filtered deck in the V2 scheduler no longer unsuspends
  suspended cards inside it.

- Fix incorrect delay being logged when Hard is used on the first
  learning step in the V2 scheduler.

- The editor no longer modifies percent-escaped text outside of image
  tags.

- Fix an extra linebreak being left in a field when an image is
  attached to an empty field.

- Tweaks to the 'tag updated notes' feature (thanks to Erez)

- Fix cards being sorted in wrong order when added after the note was
  created (thanks to Arthur)

- Disabled elastic scrolling in webviews to work around a Qt bug.

- Don’t filter em/strong tags when pasting.

- Fix error when double-clicking the open profile button.

- Constrain image width in editor to the field width.

## Changes in 2.1.19

Released 2020-01-16, build 3c8690ae.

- Fix formatting and images getting lost when creating cloze
  deletions.

- Added an option to the preferences screen to strip formatting by
  default.

- Fix the preview button shortcut key not working.

## Changes in 2.1.18

Released 2020-01-14, build fb9d59fe.

- Fixed Anki failing to start for some users updating from Anki 2.0.

- Fixed the alternate Windows build failing to start on Windows 8.

## Changes in 2.1.17

Released 2020-01-11, build c69ccb50.

Linux version repackaged on 2020-01-12 to fix a 'make install' issue.

- Improved the performance of the browse screen’s sidebar for users
  with many decks/tags.

- Add-ons that modify the sidebar will break when you update, and will
  need to be updated by the add-on author.

- Add-ons that alter the audio handling may need to be updated, as
  code has moved from anki.sound to aqt.sound.

- Changing large note types is significantly faster.

- Added an option in the preferences screen to adjust the user
  interface size.

- You can now double-click on an .ankiaddon file to install it (thanks
  to Glutanimate).

- Updated GUI libraries for the standard installs and the alternate
  Windows install.

- The minimum Python version is now 3.7, and the packaged versions
  ship with Python 3.8.

- The alternate Linux build has been dropped - you will need to be on
  a Linux distro from 2016+ with systemd support to use the packaged
  version.

- Source tarballs are available from the releases tab of the GitHub
  repo.

- Added an option to tag updated notes when importing (thanks to
  Erez).

- Automatically remove ':' from field names when opening the card
  templates screen, as it conflicts with the template syntax.

- Fix a bug in the handling of MathJax+Cloze (thanks to Michal).

- Fixed a regression in the way duplicate deck names were handled.

- Remove help button from some Window titles.

## Changes in 2.1.16

Released 2019-12-12, build 4bc33e2f.

Due to some minor issues that were found, the website was not updated to
point to this release.

- Pasting now includes formatting by default.

- Preserve foreground/background color when pasting.

- Preserve bold/italic/underline when pasting from Google Docs.

- When pasting with the shift key, bold/italics/underline is also
  stripped.

- Ensure learning cards in filtered decks with 'order due' show in
  template order.

- Remove the 'experimental' label from the new scheduler.

- You can now import and export decks with scheduling enabled in the
  new scheduler.

- Hide empty Default deck in deck picker (thanks to Arthur).

- Add an extra day to the interval when using Easy on a relearning
  card.

- Preserve surrounding styling when making cloze deletions.

- Draw preview screen more quickly.

- Fix race condition in preview screen (thanks to Håkon).

- Use --exact with dvsvgm to prevent truncated subscript/superscript
  in LaTeX.

- Newly created cards could be given the wrong due number (thanks to
  Arthur).

- Sticky fields were ignored when closing the add card window (thanks
  to Arthur).

- Adding a note type forced a full sync (thanks to Arthur).

- Remove shortcut keys from translations (thanks to Arthur).

- Documentation changes for translators (thanks to Arthur).

- Case not being preserved when changing a deck’s parent (thanks to
  Arthur).

- Hide default deck in other screens when empty (thanks to Arthur).

- Fix qtwebengineprocesses not being cleaned up when stats window
  closed.

- Allow smaller window when editing current card.

- Support pasting multiple URLs at once.

- Add ability to force software rendering on old Macs (thanks to Mike)

- A fix for case insensitive field name handling in find&replace
  (thanks to lovac42)

- Fix non-integer intervals being imported from Mnemosyne (thanks to
  Blauelf)

- Clear undo queue when changing scheduler (thanks to lovac42)

- Default to not closing add window (thanks to Aidan)

- Sort new cards separately when sorting by ease (thanks to Arthur)

- Fix a bug in the V2 scheduler.

- Properly handle backslashes in the replacement section of
  Find&Replace.

- Various small fixes.

## Changes in 2.1.15

Released 2019-08-22, build 442df9d6.

- The V2 scheduler now fully randomizes review cards due on a given
  day.

- Fix add-ons errors on Windows when profile path was short.

- Fix flag changes in Browse screen not syncing.

- Cleanup recording wav file when recording canceled.

- Fix the window icon on Wayland (thanks to Wilco).

- Add a progress bar to media deletion.

- Other minor changes.

## Changes in 2.1.14

Released 2019-06-27, build 7b93e985.

- Fix a bug in the V2 scheduler that would cause partially learnt
  cards removed from filtered decks to revert to an earlier state.

- Fix a bug in the handling of relearning cards when switching back to
  the V1 scheduler.

- Fix lost space when pasting indented text.

- Limit image height relative to window height, not document height.

- Fix deck list being re-rendered unnecessarily.

- Remove the 'unable to connect to local port' message.

## Changes in 2.1.13

Released 2019-05-20, build 3ba55990.

- Fix formatting getting lost when copying&pasting between fields on
  macOS.

- Fix some issues that cause the main window to get stuck.

- Fix an empty deck list sometimes appearing when restoring from a
  backup.

- Fix Anki hanging after an error occurs during startup.

- Fix error caused by profile with trailing space on Windows.

- Fix error message when syncing with an unconfirmed email address.

- Use jsonschema for add-on manifests (thanks to Erez).

- Warn in DB check when high due numbers are encountered.

- Improve error messages on full disk and failed add-on deletion.

- Fix relearning cards being given learning step count in V2
  scheduler.

- Fix preview window failing to appear when 'show both sides' enabled.

- Removing trailing BR tag when pasting into an empty field.

- Don’t throw an error when non-Latin text in the Javascript console
  can’t be shown.

- Double click on add-ons to edit their configuration (thanks to
  lovac42).

- Fix the window icon in a few screens (thanks to John).

- Don’t highlight the deck selection button in the add screen on
  Windows.

- Improve the default 'type in the answer' note type.

## Changes in 2.1.12

Released 2019-04-23, build eef86bf3.

- Fix an issue that could prevent profile renaming/deletion on
  Windows.

- Fix fields appearing under editor buttons.

- Fix memory leak in card layout screen.

- Fix some issues with previewing in the Browse screen.

- Fix card counts not updating when a review is undone.

- Fix an error that could occur on startup on some Windows installs.

- The Mac build now uses the new hardened runtime on Mojave.

- Change focus outline colour on Windows.

- Fix an error caused by missing note types.

- A possible workaround for the audio player getting stuck on Macs.

- Display the installed version in the Windows uninstall screen.

- Fix an issue checking for add-on updates (thanks to Glutanimate).

- Disable add-on config button when not appropriate (thanks to
  Glutanimate).

- Tweaks to the 'deck age' graph binning (thanks to Jian).

- Add-ons hosted on AnkiWeb can now define conflicts in the manifest
  file.

- Switch to mplayer on the alternate OS X build, as mpv was not
  working on some older machines.

- Make sure mpv doesn’t attempt to load scripts from default location.

- Other minor fixes.

## Changes in 2.1.11

Released 2019-03-11, build 3cf770c7.

- Change Undo shortcut back to Ctrl+Alt+Z/Cmd+Opt+Z in Browse screen,
  to prevent accidentally undoing non-text changes when editing
  fields.

- Revert a previous card template optimization that could cause an
  error.

- Suppress a spurious error message that could occur when editing.

## Changes in 2.1.10

Released 2019-03-07, build 22d6feed.

- Add option to strip html in export.

- Avoid nbsp for single spaces when pasting text.

- Fix preview screen flashing when moving between cards.

- Improvements to the add-ons screen (thanks to Glutanimate).

- Support .ankiaddon bundles (thanks to Glutanimate).

- Improve subpixel antialiasing on some machines (thanks to
  Glutanimate).

- Improve Japanese interface font on Windows 10, and make it possible
  for translators to change the font for other languages that need it
  as well.

- Fix inability to start if problem occurs on first run.

- Allow decreasing daily limits in custom study.

- Add a button to copy debug info to about screen (thanks to
  Glutanimate).

- Fix problem running from source on Windows (thanks to dlon).

- Allow add-ons to serve files from mediasrv (thanks to Glutanimate).

- More user-friendly error messages for some network errors.

## Changes in 2.1.9

Released 2019-02-20, build ae67c976.

- Update standard build to latest toolkit version.

- Hardware acceleration defaults to off again on Windows/Linux, due to
  the issues it was causing some users. If you were not experiencing
  any issues, turning hardware acceleration back on in the preferences
  screen is recommended.

- Various statistics fixes for the V2 scheduler, including an
  automatic remapping of button 2/3 in the review history when moving
  back and forth between scheduler versions so the "answer buttons"
  graph displays correctly.

- Fix BR tags being included in empty fields (thanks to David and
  zjosua)

- Optimize card template repositioning (thanks to Arthur)

- Fix a crash when copying/cutting with an empty selection (thanks to
  David)

- Avoid screen flash when undoing reviews.

- Make sure info/warning dialogs appear on top.

- Fixed an issue with just-typed text not being saved when using the
  mouse to save/add a card.

- Added support for \\{{CardFlag}}, which is either empty, or in the
  format "flagN" where N is 1-4.

- Fix bulk flag changes in Browse screen not syncing.

- Fix advanced menu in editor not showing shortcut keys.

- When UI fails to load after resuming computer from sync, show a
  tooltip and automatically refresh.

- Clean up old mplayer instances after a crash so that profile
  renaming works.

- Fix add-on list not refreshing when toggling enabled in latest
  toolkit.

- Fix cursor jumping on first click in "Edit Current" area on Windows.

- Preserve whitespace when pasting plain text.

- Prevent errors caused by a timer firing after collection is
  unloaded.

- Ensure a full sync is forced when restoring from a backup.

- Ensure full window is on screen when displaying windows on a changed
  screen layout.

- Improvements to the add-ons, debug console, and error screens
  (thanks to Glutanimate)

- Ensure \\{{Deck}} shows the correct deck when adding (thanks to
  Arthur)

- Ensure windows don’t get shown off-screen.

- Remember add-on window size and position.

## Changes in 2.1.8

Released 2019-01-02, build 71e0c880.

- Fix startup on Windows 8.

- Fix field content appearing under editor buttons.

- Better handle an error when recording.

- Fix improper handling of collections with deck errors.

- Fix duplicate deck names being created due to text encoding.

- Fix gtk2 theme and fcitx module not being included.

- Detect nouveau graphics drivers and automatically switch to software
  rendering.

## Changes in 2.1.7

Released 2018-12-17.

- Fix "QPushButton has been deleted" error messages after a problem
  occurs changing note types.

- Fix errors during "Check Database" that are just a byproduct of a
  previous operation that failed.

- Fix problems searching for some non-Latin text in decks/note type
  names.

- Ensure cgi and uuid modules are available to add-ons.

- Improvements to the Windows installer.

- Automatically restart mpv if it stops responding.

- Don’t convert non-Latin characters in add-on configuration to
  difficult-to-read escape codes.

- Add a bottom border to the menubar on Windows 10.

## Changes in 2.1.6

Released 2018-12-10.

Downloads are now split into a standard and alternate version.

**The standard version**:

- Is built with the latest toolkit, which fixes various issues.

- Changes the undo shortcut back to Ctrl+Z or Command+Z like Anki 2.0.

- Includes a separate anki-console.exe executable in the Windows build
  that may be useful for add-on authors.

- Includes support for the fcitx input method and a gtk2 theme in the
  Linux build.

You can switch between the standard and alternate 2.1.6 without
problems. If you move back to a previous Anki 2.1 release, your sync
login details and window positions will be lost, and will need to be set
again.

**The standard version has updated requirements**:

- The Windows build only supports 64 bit Windows 7 or later, and will
  not run on a 32 bit install.

- The Mac build requires macOS 10.12 or later.

- The Linux build requires a Linux distribution from approximately
  2016 or later.

The alternate version is similar to previous Anki 2.1 releases, and is
built with an older toolkit. It will run on some older systems that the
standard version will not, but as it is not as up to date, it may be
missing bugfixes and security improvements that the standard version
includes.

**The alternate version will run on**:

- Windows 7 32 bit or 64 bit installs

- Mac 10.10 or later.

- A Linux distro from around 2014 or later.

**In addition to the toolkit upgrade, there have been some changes in
Anki itself**:

- Improvements to the Browse screen and flagging:

  - Search text is normalized, which fixes problems searching for
    unicode characters with multiple possible encodings.

  - The selection is now partially transparent, allowing you to see
    the underyling colours of the rows.

  - The screen doesn’t scroll when performing actions that don’t
    change the selection count.

  - Flags now toggle on and off, and the separate clear flag action
    has been removed.

  - The second flag is now orange instead of purple.

  - Find&replace now only shows fields relevant to the notes you’ve
    selected, and is case insensitive.

  - Fix card list not updating when editing HTML.

- Importing apkgs is now more verbose about how notes have been
  handled.

- Prevent errors caused by the user adding a field reference to itself
  on a field.

- Better handle issues with the deck list, such as decks that are
  missing a parent deck.

- Anki should now be able to function even if a system proxy is
  configured for localhost connections.

- Fix font size being copied when pasting between Anki fields with
  bold text.

- Pasting a link with shift held down now creates a clickable link.

- Fixed an issue with the bulk remove tags option where tags with
  similar names could be removed as well.

- Fixed an error that occurred with very long filenames on Windows.

- Fixed an issue running latex commands on some Linux installs.

- The Browse screen’s sidebar now defaults to on.

- Fixed a race condition that could cause two copies of Anki to open.

- When adding media to cards, Anki now will automatically rename the
  filenames if they’re too long.

- The experimental scheduler now regularly checks if new learning
  cards have become due.

- Handle invalid add-on config (thanks to Arthur).

- Enforce template ordering when card templates are reordered after
  card creation (thanks to Arthur).

- Don’t change deck when Esc pressed in deck chooser (thanks to
  David).

- Fix a problem on initial startup when English not the default
  language.

- Fix busy cursor showing in import results screen.

- Fix content overlap when add-ons have added many editor buttons.

- Don’t change current note when reopening editor from review screen
  (thanks to Arthur).

- A fix for running on Python 3.7 (thanks to Alexey).

- Restore the tooltip for the Fields and Cards buttons in editor.

- A possible fix for 'database is locked' errors on Windows.

## Changes in 2.1.5

Released 2018-10-01.

- Use selected answer button instead of default when enter/space
  pressed.

- Change undo shortcut in browse screen to avoid conflict with editing
  functionality.

- Ignore standard mpv config file location in favour of Anki data
  folder.

- Fix importing of .apkg files when interface in Dutch.

- Fix translations not working on Linux after 'make install'.

- Support newlines in type:cloze, and treat them as spaces.

- Add browser.rowChanged hook for add-on authors.

- Possible fix for some 'database is locked' errors.

- Fix errors on startup when deck given an invalid name.

- Fix sorting not working when field contains only a media reference.

- Fix 'access denied' error not being caught properly.

- Fix exporting of v2 colpkg when interface in non-English language.

- Fix conditional replacement not ignoring HTML formatting.

- Fix question fade time being forced when hardware acceleration on.

- Add a small margin between buttons during review.

- V2 scheduler now respects maximum interval even if it will lead to
  all buttons giving the same interval.

- Tweak margins in overview and answer button areas.

- Ignore UI events that are received after collection has been closed.

- Don’t try to import .anki(2) files as text.

- Added support for Lojban (thanks to giqtaqisi)

## Changes in 2.1.4

Released 2018-09-05.

- Fix deck list getting stuck when creating filtered deck.

- Prevent local cards being overwritten when accidentally downloading
  empty AnkiWeb collection.

- Favour mark/flag colour over suspended colour in browse screen.

- Fix new day calculation in experimental scheduler.

- Linux theme tweaks (thanks to Glutanimate).

- Disable view page button for locally added add-ons (thanks to
  upday7).

## Changes in 2.1.3

Released 2018-08-30.

- Hardware acceleration can now be toggled in the preferences screen
  on Windows/Linux.

- Disable question fade-in during review when hardware acceleration is
  off.

- Fix some add-ons leaving a blank space in the main window when Anki
  restarted.

- Fix file associations on macOS.

- Fix some unwanted text being included when pasting.

- Fix shortcut keys like space from repeatedly triggering when held
  down.

## Changes in 2.1.2

Released 2018-08-20.

- Add missing .apkg and .colpkg file associations.

- Improve handling of images inlined in fields.

## Changes in 2.1.1

Released 2018-08-09.

- Fixed exporting of .apkg files with regular scheduler.

- Work around Anki failing to start on some Windows machines.

- Fix dialogs failing to show in tabs when using macOS’s full screen
  mode.

- Extract embedded images when pasting HTML.

- Fix images copied from Finder not pasting properly.

- When the sort field is set to RTL, display in RTL order in the
  browser.

- Update toolkit version on Windows.

## Changes in 2.1.0

Released 2018-08-06.

The first stable release of Anki 2.1.

Changes from the previous release candidate:

- Don’t unmaximize when reshowing browse screen.

- Add \*.webm to attach media file selector.

- Add shortcut key for MathJax mhchem support.

## Changes in Anki 2.1

### Translations

- [日本語](http://rs.luminousspice.com/changeinanki2/)

### At a glance

- Anki 2.1 uses the same scheduling, syncing and file format as Anki
  2.0.x, so you can upgrade and downgrade at will.

- It’s built with recent support libraries (Python 3.6, Qt 5.9/5.12),
  bringing fixes for crashes, better handling of high resolution
  displays, non-Latin text, and the latest web standards.

- It requires a modern system - Windows 7+, OSX 10.10+, or a Linux
  distro from around 2014+.

- Add-ons will need to be updated to work with 2.1.

### Add-ons

Add-ons need to be updated to work with Anki 2.1. [Some
add-ons](https://ankiweb.net/shared/addons/2.1) have already been
updated; others have not been ported yet.

When you install 2.1, it will create a separate folder for add-ons, and
not import any existing ones you have installed.

If you’re an add-on author, you can read more about the required changes
on <https://apps.ankiweb.net/docs/addons.html>

### Other changes

Anki 2.1 brings numerous bugfixes, and some quality of life
improvements, such as:

- Built in MathJax support

- A "restore backup" option in the profiles screen

- SVG rendering support for LaTeX

- Improved add-on configuration, management and updating

- Night mode for reviewing

- Improved pasting, with less unnecessary formatting included, and
  better handling of media links. You can hold the shift key when
  pasting to allow more formatting to be included.

The Browse screen has been simplified:

- Various shortcuts that were previously in the sidebar are now
  available via the Filter button. If you find yourself frequently
  accessing certain items, you can save the search to have them appear
  in the side bar.

- The top bar with common shortcuts has been removed. You can access
  all actions quickly by right clicking or ctrl+clicking in the card
  list instead, and there is an add-on available for adding back the
  top bar if you still prefer it.

A full list of changes made during the alpha and beta period are
documented [here](https://apps.ankiweb.net/docs/beta.html).

### Experimental scheduler

Anki 2.1 contains an optional, [experimental
scheduler](https://anki.tenderapp.com/kb/anki-ecosystem/experiment-scheduling-changes-in-anki-21).
The experimental scheduler is not compatible with older Anki versions.
