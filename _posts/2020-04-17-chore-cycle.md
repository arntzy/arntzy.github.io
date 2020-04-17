---
layout: post
title: "Chore Cycle"
date: 2020-04-17 16:43:00
description: Use this spreadsheet to cycle chores in the quarantimes
share: true
tags:
  - google sheets
  - google apps script
---
[![img]({{ '/assets/img/chore_cycle.png' | relative_url }}){: .center-image }*just look at this sheet*]({{'/assets/img/chore_cycle.png' | relative_url}})

___
# why with this sheet

- I hate cleaning; I love clean.
- I hate overwhelming stressful task; I love bite-sized atomic task.
- I hate...lamp?; I love Golden Gate Bridge.

I love the Golden Gate Bridge because it is always being painted. When the painters reach the end of the bridge, they start over again at the beginning. The GGB is never not being painted.

I wanted to take the GGB approach to cleaning our apartment while we are locked down in the quarantimes. The fairest way to achieve a clean apartment without being stressed out is to cycle chores between me and my partner on a weekly basis with a couple cleaning tasks every day.

Our apartment has never been so clean because it is never not being cleaned.

___
# what is this sheet

After modifying your copy of this spreadsheet, you can run the choreCycle function to cycle the chores for the next week. You can continue to edit and change the behavior of your copy to your liking. Use this sheet to see who needs to do what chores each day and live that _#nevernotcleanlyfe_. Go wild!

## technical bullsheet (skip if you are feeling tldr)

When I am designing and implementing spreadsheets for my own personal use, I always aim for rows to contain all the input necessary to be processed by a pure function. In this way, adding additional rows or sorting order (within your defined range) doesn't affect the functionality of the sheet. This sheet is no different; each row describes a task, the room/type of task, and has either a checkbox or a 'Week Tally' (to be explained below).

Here are some features used in this sheet:

- **Google Apps Script (GAS)**

  - I wanted the chore cycling to be done automagically without the requirement of knowing how it works. You can write custom functions or whole scripts using JavaScript (kinda) running on a V8 engine in the cloud.
  - Like anything else here, feel free to modify your own script by going to `Tools > Script Editor`.
  - If you have found a better way to code any of these functions make a [pull request](https://github.com/arntzy/Chore-Cycle) and I will update the code on the shared sheet for people making copies in the future. Google has its own versioning for the .gs files, but I would prefer to use git and github even though it involves manually copying the scripts into the sheets script editor for now.

- **Named Ranges**

  - After making modifications to the tasks on the sheet, a user can set the new ranges on the sheet itself instead of modifying code. View/Edit the Named Ranges at `Data > Named ranges`.

- **Scheduled Time-Based Trigger (Cron-like)**

  - Much to my delight, you can execute a GAS function or script automatically in the cloud on a regular basis.
  - You can see the triggers in the script editor (`Tools > Script Editor`) at `Edit > Current project's triggers`.

- **Macros**
  - I imported the main function to execute as a macro which is bound to the keyboard shortcut `Ctrl`{: .key}+`Alt`{: .key}+`Shift`{: .key}+`1`{: .key}. On a mac: `Cmd`{: .key}+`Option`{: .key}+`Shift`{: .key}+`1`{: .key}
  - Even though cycleChores() will automatically execute on the time-based trigger, you can execute it locally to test and check for configuration errors.
  - You can view macros at `Tools > Macros`.

___
# how to use this sheet

### 1. Install

- Make a copy of this [sheet](https://docs.google.com/spreadsheets/d/1kO8fvWP9GukuoiwqLK5amuojOx1IbEPJSk3klVSGQKI/copy){:target="_blank"}.
- Rename your new copy to whatever the hell you want.

### 2. Customize your sheet with chores and people

- You won't have to do this step more than once. (But of course, you can always tweak!)
- The template is set up with a person A and a person B for each day. Rename them if you want, or add more people to the cycle by adding columns and horizontally merging the DOTW cells in row 1. These things are up to you.
- Column A can be modified with whatever you want to organize your tasks.
- Add Checkboxes on the days you want to do the chores with `Insert > Checkbox`.

### 3. Add Irregular Interval Chores (IICs)
[![img]({{ '/assets/img/irr_chores.png' | relative_url }}){: .center-image }*this sheet ain't regular*]({{'/assets/img/irr_chores.png' | relative_url}})
- Sometimes we might want to add a chore that is only done once every two weeks or once every four weeks (The code currently only supports these two situations, but is easily extensible to once every 3 or 5 or 12...whatever).
- Add as many of these tasks as you want to the sheet in the section below the main weekly chore cycle.
- Populate days with a single X to start the Week Tally counter for that chore.
- When the cell shows the number of XX's indicated by the chore type, i.e. 'XX' for two-week chore, 'XXXX' for four-week, that's when the chore should be completed.

### 4. Set Named Ranges
[![img]({{ '/assets/img/named_ranges.png' | relative_url }}){: .center-image }*it is what it is*]({{'/assets/img/named_ranges.png' | relative_url}})
- Unhide column D by clicking one of the two arrows in D1 (Column D is there to act as a temp clipboard for move/copy/paste reasons).
- Go to `Data > Named ranges`.
- Edit the Named ranges to match your new sheet. I will eventually clean these up and calculate them for you, but for now they need to be set manually. Hopefully once you get a good chore cycle in place, you won't have to modify these very much.
- Named Ranges Descriptions
  - **chore_clpbrd:** D column, as many rows as weekly chores
  - **chore_clpbrd_paste:** Last column of weekly chores range, as many rows as weekly chores
  - **chores:** Whole weekly chore range not including column D (CLIP)
  - **four_week:** Whole four-week chore range not including column D (CLIP)
  - **moved_chores:** Whole weekly chore range INCLUDING column D (CLIP)
  - **total_irr_with_clpbrd:** Whole irregular interval chore range (for now, just the two-week and four-week chores) INCLUDING column D (CLIP)
  - **two_week:** Whole two-week chore range not including column D (CLIP)
- Re-hide Column D. You don't need it anymore

### 5. Modify Time-Based Trigger (Optional)

- If you want to set up a trigger to run the script automatically each week, you can set a time-based trigger by going to the script editor at (`Tools > Script Editor`) and then in the script editor `Edit > Current project's triggers`.
- Click the button to '+ Add Trigger'
- Make the form look like this:
  [![img]({{ '/assets/img/triggers.png' | relative_url }}){: .center-image }*sheetin' the sheet*]({{'/assets/img/triggers.png' | relative_url}})
- Click 'Save' and you have a trigger.
- You may need to go through the steps of allowing access from the script to modify the data on your copy of the spreadsheet, which arrives as a pop-up window. No worries.
  
### 6. Test the cycleChores Macro

- Execute the macro to watch the cycle happen once with `Ctrl`{: .key}+`Alt`{: .key}+`Shift`{: .key}+`1`{: .key}. On a mac: `Cmd`{: .key}+`Option`{: .key}+`Shift`{: .key}+`1`{: .key}
- Undo all the changes until you are back to your starting sheet.
- If everything behaved as it should, you now have a working sheet.

### 7. Get to work and enjoy the cleanest apartment you have had in years!
___
# troublesheeting

- Double check your Named ranges are correct
