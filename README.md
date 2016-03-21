# CNBT

A collection of all command-relevant NBT data for Minecraft 1.9.1, sorted based on inheritance.

#Parameters

Keys for sorting and defining information.

##Root

1. `"<group>"` = A grouping of classes. Currently only "entity", "block", "item", and "misc".

###\<group\>

1. `group > name` = String. Name of the class.

2. `group > parent` = String. The name of the class within the group that this class will inherit all `tags` from, including grandparents and onwards.

3. `group > id` = Integer. The numerical ID of the class. Only relevant when `savegame` is true.

4. `group > savegame` = Boolean. Whether or not `name` is the savegame ID for the class. If false, it is neither its savegame ID nor is it saved to disk. Defaults to true.

5. `group > disk` = Boolean. Whether or not the class is saved to chunk files. Irrelevant if `savegame` is false. Defaults to true.

6. `group > ignoreInheritance` = Boolean. Only relevant to the "entity" group. If true, the current class will **not** inherit `tags` from parents/grandparents, but **will** still inherit from the "Entity" class. Defaults to false.

7. `group > eggColors` = Array of integers. 2 integers defining primary and secondary colors for eggs. Only relevant for the "entity" group.

8. `group > tags` = Array of objects. List of tag data that the class uses.

9. `group > inherit` = Array of strings. A list of classes that this class will optionally inherit tags from (including parents/other inherited data). Syntax is "group:class". Excluding "group" will use the group of the current class.

####tags

1. `tags > id` = String. The name of the tag.

2. `tags > type` = String. The datatype of the tag. One of the following: Byte, Short, Integer, Long, Float, Double, String, IntArray, Compound, List, List/<datatype>. Note that "ByteArray" is missing because it cannot be declared via in-game NBT data.

3. `tags > isBoolean` = Boolean. Whether or not the value is treated as a boolean. There is currently no "Boolean" datatype, as it is technically saved as a "Byte". Defaults to false.

4. `tags > forced` = Boolean. Whether or not creation-commands (`/summon`, `/entitydata`, `/setblock`, `/give`, etc.) requires the datatype of the tag to be declared. Only relevant for numerical datatypes Byte, Short, Integer, Long, Float, Double. Note that testing commands (`/scoreboard`, `/testfor`, `/testforblock`, etc.) requires correct declaration no matter what. All other datatypes (String, IntArray, Compound, List) requires correct declaration, while Lists requires internal data to be specified correctly. Defaults to false.

5. `tags > deprecated` = String. Specifies the name of the tag that overrides this one, indicating deprecation. If null, tag is not deprecated. Defaults to null.

6. `tags > minValues` = Array of doubles. The minimum value for tag input. Each index corresponds with the tag's input index. A value of `minValues:[-180.0,-90.0]` means the first value within the input List tag must have a minimum value of -180.0, while the second value must have a minimum of -90.0. The minimums will repeat if there are more values defined in the List tag than there are in the `minValues` array (provided the `keyLimits` are not exceeded). If it's just a single-value tag, such as a Short, only one value is necessary in the array and the rest are ignored. If empty, no minimum values. If any value within the array is null, no minimum for that index.

7. `tags > maxValues` = Array of doubles. The maximum value for tag input. Each index corresponds with the tag's input index. A value of `maxValues:[180.0,90.0]` means the first value within the input List tag must have a maximum value of 180.0, while the second value must have a maximum of 90.0. The maximums will repeat if there are more values defined in the List tag than there are in the `maxValues` array (provided the `keyLimits` are not exceeded). If it's just a single-value tag, such as a Short, only one value is necessary in the array and the rest are ignored. If empty, no maximum values. If any value within the array is null, no maximum for that index.

8. `tags > correctedValues` = List of doubles. The value to reset the index of input to if it exceeds the values defined within `minValues` or `maxValues`. If any value within the array is false, value will be corrected to either `minValue` or `maxValue` as defined. If `correctedValues` is empty or not defined, or a value is null, tag value input will not be corrected.

9. `tags > permissions` = Object. Holds data for generic permissions usage.

10. `tags > permissions > read` = Boolean. Whether or not the tag is read from NBT (`Team`, for example, is **only** read, not written), making it possible to specify for creation. Defaults to true.

11. `tags > permissions > write` = Boolean. Whether or not the tag is written to NBT, making it possible to specify for testing. Defaults to true.

12. `tags > permissions > saveOnly` = Boolean. Whether or not the tag is **only** relevant when saved to chunks. A much more technical reasoning behind it. For example, the "Entity" class data supersedes basic NBT reading/writing, but the `id` tag is only a part of chunk-saving functions and is not actually a part of input or output from reading/writing. If true, ignores whatever `read` and `write` are set to as they will both be assumed false. Defaults to false.

13. `tags > keyLimit` = Object. Holds data for List tag restrictions.

14. `tags > keyLimit > min` = Integer. Minimum number of keys that must be defined within the List tag. If 0, no minimum. Defaults to 0.

15. . `tags > keyLimit > max` = Integer. Maximum number of keys that must be defined within the List tag. If 0, no maximum. Defaults to 0.

16. `tags > tags` = Array of objects (recursive). Used for Compound and List/Compound tags to specify deeper-nested tags.

17. `tags > inherit` = Array of strings. A list of classes that this Compound or List/Compound will optionally inherit tags from (including parents/other inherited data). Syntax is "group:class". Excluding "group" will use the group of the current class.

