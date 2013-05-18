# Virtual Value List

Virtual Value List helps developers build transient value lists based on the contents of global variables. By basing value lists on global variables, developers can be spared most of the schema overhead associated with other techniques for value lists with programmatically specified values.

## Attributions

This module is based on value list demos by [John Ahn][1] and [Andries Heylen][2], and a technique by [Marcelo Piñeyro][3] for coercing value list ordering. [Joel Shapiro][4] discovered and reported significant bugs in earlier versions of this module.

[1]: http://www.filemakerhacks.com/?p=5357 "FM 12 ExecuteSQL 'Unconference' Session"
[2]: http://www.filemakerhacks.com/?p=5412 "Magic Value Lists"
[3]: http://www.soliantconsulting.com/blog/2012/09/extending-filemaker-pro’s-value-list-sort-capabilities-using-char-function "Extending FileMaker Pro's value list sort capabilities using the Char() function"
[4]: http://jsfmp.com "Joel Shapiro"

## Installation

You must use a copy of FileMaker Pro Advanced to install the custom functions for this module.

1. Import all the custom functions to your solution file.
2. Copy or reproduce the VirtualValueList table into your file.
3. Reproduce the relationship between the VirtualValueList and VirtualValueList__related table occurrences in your file.
4. Import the "Virtual Value List" module script folder into your file.
5. Edit the "Go to Virtual Value List Layout" script to go to a layout in your file based on the VirtualValueList table occurrence.
6. Add the "Enforce Virtual Value List Record Requirement" script as a sub-script of your file's startup (OnFirstWindowOpen) script.
7. For each value list you anticipate using simultaneously in your solution, mimick one of the value lists from this file. Choose which value list to mimick based on whether you need that value list to set a hidden ID value or not.

You will need to create new fields in the VirtualValueList table for each virtual value list you create.

For each value list you create, FileMaker will warn you that value lists on unindexed fields don't work. Don't worry; these value lists work if they are set-up correctly.

## Usage

See the demos in this repository for examples of how to set-up virtual value lists in your solutions.

To use Virtual Value List with pop-up menus and drop-down lists:
1. Select one of the virtual value lists to associate with the pop-up menu or drop-down list.
2. Add to the field an OnObjectEnter script trigger calling the "Exit Script OnTrigger with Parameter as Result".
3. In the script parameter to the OnObjectEnter script trigger, use the VirtualValueListSet custom function to set the virtual value list values to use with the field. If you're using ExecuteSQL to get the values to set, the VirtualValueListSliceAndSet function may be worth considering instead of the VirtualValueListSet function.
4. As a best practice, add to the field an OnObjectExit script trigger calling the "Exit Script OnTrigger with Parameter as Result" script.
5. In the script parameter to the OnObjectExit script trigger, use the VirtualValueListClear custom function to clear the virtual value list. This cleans-up the global variables used to drive the virtual value list, which is no longer needed when the field is exited.

To use Virtual Value List with radio button and checkbox sets:
1. Select one of the virtual value lists to associate with each radio button or checkbox set.
2. Use an OnLayoutEnter or OnModeEnter script trigger to set each virtual value list via the VirtualValueListSet custom function. If you're using ExecuteSQL to get the values to set, the VirtualValueListSliceAndSet function may be worth considering instead of the VirtualValueListSet function.
3. As a best practice, consider using the VirtualValueListClear function with an OnLayoutExit script trigger to clear a virtual value list when leaving a layout using the value list.

You can set up as many Virtual Value Lists in your solution files as you want. Use the virtualValueListID parameter of the custom functions to address different value lists. The numbering scheme to use with virtualValueListIDs is up to you, and you can make it whatever you want. This does not have to be FileMaker's internal ID for the value list (but that's not a bad idea!).

## Configuration Options

For value lists with hidden ID values to work correctly, the VirtualValueList table must have at least as many records as the largest such value list. Edit the "Get Virtual Value List Settings" script to set the number of VirtualValueList records to use with your solution.

## License

Anyone may do anything with this software. There is no warranty.