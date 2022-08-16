# Solution Notes
- Created basic layout
- Created reusable styles for buttons, text, variables/mixins
- Broke video/capture/both into separate child components of Video component
- Made SourceControls component (need to make buttons dynamic)
- Made MediaModal to add media to scene
- Added buttons to each added media source to turn on/off
- Hooked up show/hide for video source
- Set up layout options for video source
- Hooked up show/hide for screenshare source
- Set up layout option for screenshare
- Created SVGs of icons (super fast and renders much crisper)
- Hooked up show/hide buttons for video and/or screenshare
- Set up layout options for 3 video/screenshare and hook buttons to toggle it
- Kept code as simple as possible for the first pass

## Possible Enhancements
- Would create data objects on a second pass to make components more concise and reusable, particularly for the layout buttons.
- Would simplify the CSS a bit more so it's more readable

## How long did it take you to complete this assignment?
Between 4 and 6 hours

## What about this assignment did you find most challenging?
The most challenging part about this assignment was making educated guesses around the styling since I
didn't have access to see the spacing/fonts/etc in the Figma file.

## What about this assignment did you find unclear?
Once I read through the assignment and looked through the Figma files, this assignment seemed pretty clear.

## What challenges did you face that you did not expect?
A challenge I faced as just managing all of the various use-cases and making sure everything worked as intended.

## Do you feel like this assignment has an appropriate level of difficulty?
I believe it was an appropriate level of difficulty.

## Briefly explain your decisions to use tools, frameworks, and libraries like React, Vue, etc.
I chose to use Vue for this along with Sass (using the scss format) since I am relatively familiar with Vue. I 
also used Sass to manage the CSS since I could pre-define variables and mixins for code reuseability and easily 
swapping out styles at need.

## Did you make certain assumptions and decisions around the UI/UX? Please elaborate on your reasonings.
I made some assumptions about the UI/UX in that I chose a default aspect ratio of 16:9 for the video portion as 
well as the media buttons since it is a bit of a standard. I also added some basic error messaging as well as a 
'Close' button if the user has already added the camera source or screenshare source.
