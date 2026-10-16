# Social Media Planners v1.0.0
This toolkit automatically analyses your video transcripts (SRT files) and produces a ready-to-use Video Editors cut plan

1. What This System Does
This toolkit automatically analyses your video transcripts (SRT files) and produces a ready-to-use Video Editors cut plan.

It finds the best short clips, flags dead air / fillers, suggests strong hooks, and writes clean marker files you can import.

2. Folder Structure

























FolderPurposeD:\Road2Abong-CameroonSource videos + raw transcripts (Episode-XX_raw.srt)C:\YouTubeStudio\toolsAll scripts and the config fileC:\YouTubeStudio\transcriptsClean copies of the transcriptsC:\YouTubeStudio\plansOutput cut plans, CSVs and marker files

3. Main Features
Core Planner (Get-CutPlan.ps1)

Auto-detects SRT, Whisper and bracket-style transcripts
Scores every segment using:
Word density (log-smoothed)
Hook keywords
Numbers & punctuation
Filler detection (built-in list + auto-learned)
Duration preference (ideal ≈ 4 seconds)

Flags issues: dead-air gaps, low-density speech, pure fillers
Selects top recommended cuts + best hook candidates
Writes three outputs per episode:
Episode-XX.txt – human-readable cut plan
Episode-XX.csv – full segment data
Episode-XX_markers.csv – ready for Filmora markers


Config (cutplan.config.json)

Fully tunable scoring weights
Custom filler phrases and hook keywords
Auto-learn fillers from the current transcript
Target duration / number of cuts

Launchers

























Script / BatchWhat it doesRUN-ME-FIRST.bat + Plan-Latest.ps1Processes only the newest *_raw.srt onceRUN-ME-FIRST - Multiple.bat + Plan-Latest-Watch-Multiple.ps1Processes all existing + watches for new onesWindow title updatesShows current episode and “still alive” heartbeatClear console loggingTimestamped status messages
Extra Tool

Detect-AudioActivity.ps1 – Creates an audio energy map (silence vs speech) using FFmpeg


4. Step-by-Step Setup

Make sure the four folders above exist.
Copy all scripts into C:\YouTubeStudio\tools\.
Confirm cutplan.config.json is in the same folder.
(Optional) Run setup.ps1 once to verify everything.


5. How to Use – Daily Workflow
Option A – Process only the newest episode

Drop a new file named Episode-42_raw.srt into D:\Road2Abong-Cameroon.
Double-click RUN-ME-FIRST.bat.
Wait a few seconds → plans appear in C:\YouTubeStudio\plans\.

Option B – Process everything + keep watching (recommended)

Double-click RUN-ME-FIRST - Multiple.bat.
The script will:
Process every existing *_raw.srt (oldest → newest)
Then stay open and watch the folder

Whenever a new *_raw.srt appears, it is processed automatically.
Window title shows progress (CutPlan – Processing Episode-42, then a live heartbeat).
Press Ctrl+C when you want to stop watching.


6. Understanding the Output
Open any Episode-XX.txt in the plans folder. You will see:
text--- HOOK CANDIDATES (put one at 0:00) ---
--- ISSUES TO CUT ---
--- RECOMMENDED CUTS (top N by score) ---
--- SUMMARY ---

Hooks → best opening lines
Issues to cut → dead air, fillers, weak segments
Recommended cuts → strongest clips ranked by score

Import the _markers.csv into Filmora for instant markers.

7. Customising Behaviour
Edit C:\YouTubeStudio\tools\cutplan.config.json:

targetCuts – how many top clips to recommend
targetDuration – overall target length (informational)
fillerPhrases / hookKeywords – add your own words
scoring.minDurationSec – ignore clips shorter than this
scoring.idealDurationSec – prefer clips near this length
autoLearnFillers – automatically detect repeated one-word fillers


8. Quick Troubleshooting

























SymptomSolution“No *_raw.srt files found”Check the exact filename ends with _raw.srt and is in D:\Road2Abong-CameroonWindow title never changesYou are still using the old scripts – replace them with the fixed versionsNothing happens when using the Multiple batMake sure the bat file contains only the clean two lines (no trailing ^)Planner skips a fileCheck the transcript is valid UTF-8 SRT

9. Recommended Daily Routine

Finish recording / generate the SRT → save as Episode-XX_raw.srt in the videos folder.
Leave RUN-ME-FIRST - Multiple.bat running in the background.
When the new file appears it is processed automatically.
Open the new .txt plan and start editing in Filmora.

That’s the complete current feature set and workflow.
