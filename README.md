# excel-maze-generator
This spreadsheet generates mazes for you to print, and your children to complain about how they're not as good as the ones that you get in the pub.

![](https://github.com/pugwonk/excel-maze-generator/raw/master/result.jpg)

# Short instructions
1. Download [mazegenerator.xlsm](https://github.com/pugwonk/excel-maze-generator/raw/master/mazegenerator.xlsm)
1. Go to the `maze` sheet
1. Click "make new one"
1. Go and make a cup of tea (press Escape to cancel if you get really fed up)
1. Print it
1. Hand to child
1. Observe disappointment

# How it works
The logic for this is almost all in the spreadsheet - the macro just saves you a lot of clicking and recalculating. The workbook operates in two stages:
1. It builds a path through the grid (on the `path` sheet)
1. It builds a maze with openings where the path needs them, but random lines where it doesn't (on the `maze` sheet)
1. It tests to see how easy the resulting maze is and, if it's much easier than the path was intended to be, it goes back to step 2 until it's hard enough (on the `test path` sheet)

The final mazes will probably have multiple ways to complete them. And, as your child will point out, they're not very good.

# More about how it works

The `maze` tab generates a maze when it is recalculated. The cells randomly contain a "T" if there's a top border and a "L" if there's a left border. They're formatted white so you can't see the text in there when you print it. The maze lines are created using conditional border formatting on the cells.

![](https://github.com/pugwonk/excel-maze-generator/raw/master/mazetab.png)

The `path` tab builds a random route through a grid.

![](https://github.com/pugwonk/excel-maze-generator/raw/master/example-path.png)

The `test path` tab determines whether there's any too-easy path through the maze and the overall quality of the maze. It uses iterative calculation to generate the path.

![](https://github.com/pugwonk/excel-maze-generator/raw/master/example-test-path.png)

The four parameters you can edit are:
* `LineProb` - the probability of any grid cell having a left or top border on it. Basically the complexity of the maze (higher is more complex, lower is more sparse)
* `MinMoves` - the shortest path through the maze that will be acceptable (higher numbers mean more complicated routes)
* `MaxMoves` - the longest acceptable path. You'd think very complicated routes would be good, but actually they cause a lot of doubling-back and make blank areas in the final maze
* To change the effort in the path testing, change the number of iterations in the workbook's iterative calc settings. Higher means more complex path attempts but slower maze production

Changing either of these parameters may result in better mazes but the macro could take a long time to run. This is not the most efficient way to make a maze.

The spreadsheet does have a macro in it, but the core logic is in the spreadsheet itself. To generate a maze without using macros:
1. On the `path` sheet, Shift-F9 until `Usable` becomes `TRUE`. You now have a proposed path
1. On the `maze` sheet, Shift-F9 to make a maze that the path will get through, with some other random lines around the place
1. On the `test path` sheet, change `Reset` to be `1` (this resets the brute-force path through the maze)
1. Shift-F9 to reset the test path
1. Still on the `path` sheet, change `Reset` to be `0` and then Shift-F9
1. If there is _no_ number next to "END" in the Path grid, the maze is hard enough

You may have to do this several hundred times before you get a reasonable maze out of it, hence the macro to just perform the above steps.