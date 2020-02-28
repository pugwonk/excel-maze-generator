# gif2xlsx
This spreadsheet generates mazes for you to print, and your children to complain about how they're not as good as the ones that you get in the pub.

# Short instructions
1. Download [mazegenerator.xlsx](https://github.com/pugwonk/excel-maze-generator/raw/master/mazegenerator.xlsx)
1. Go to the "maze" tab
1. Click "make new one"
1. Go and make a cup of tea (press Escape to cancel if you get really fed up)
1. Print it

# Long description
The "maze" tab generates a maze when it is recalculated. The cells randomly contain a "T" if there's a top border and a "L" if there's a left border. They're formatted white so you can't see the text in there when you print it. The maze lines are created using conditional border formatting on the cells.

![](https://github.com/pugwonk/excel-maze-generator/raw/master/mazetab.png)

The "path" tab determines whether there's a path through the maze and the overall quality of the maze. It uses iterative calculation to generate the path.

![](https://github.com/pugwonk/excel-maze-generator/raw/master/example-path.png)

It scores the path by using the Square Scores grid - paths that go right through the middle don't score very well, and ones that go around the edges do better.

![](https://github.com/pugwonk/excel-maze-generator/raw/master/square-scores.png)

The two parameters you can edit are:
* LineProb - the probability of any grid cell having a left or top border on it. Basically the complexity of the maze (higher is more complex, lower is more sparse)
* MaxScore - the highest score you will accept as a valid maze for the macro to stop running (low scores are good, high scores are bad).
Changing either of these parameters may result in better mazes but the macro could take a long time to run. This is not the most efficient way to make a maze.

The spreadsheet does have a macro in it, but the core logic is in the spreadsheet itself. To generate a maze without using macros:
1. On the "path" sheet, change Reset to be 1 (this resets the path through the maze)
1. F9 to generate a new maze on the "maze" sheet and reset the path calculations
1. On the "path" sheet, change Reset to be 0 and then shift-F9 a few times until new cells stop populating in the Path grid
1. If there is a number next to "END" in the Path grid, the maze is solvable
1. If the score is nice and low it's a decent maze
You may have to do this several hundred times before you get a reasonable maze out of it, hence the macro to just perform the above steps.