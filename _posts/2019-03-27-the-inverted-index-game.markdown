Here is a cool game I invented to teach a class the basic idea of how an Inverted Index works (the fundamental data structure of all search algorithms). It is also a fun way to get to know the class.

The rules:

* You want to find a number of students.
* You only know their names but not their faces.
* They are not allowed to say their names.
* When asked for a specific name they can reply with Yes or No whether this is their name.

Ask the students to come up with ideas on the fastest way to find the students in question. The most obvious way of course is to just go person by person and ask them for each name on the list. At O(number of students) this is quite inefficient.

Some optimizations come to my mind: Cross names of the list once you have correctly identified someone. Skip names that do not match the person’s gender. Still, this will take a long time.

Someone might have the idea for the class to line up alphabetically. They are on to something! This works pretty well for small group. Still, in the worst case this takes a while if one of the names in question starts with a late letter like X. Starting from the back of the line is also not helpful since there may be many students with names starting with Z, who knows. And it will definitely take a long time for a dozens or hundreds of students.

Inverted Index to the rescue: How about students form lines according to the first letter of their name? This way you just need to ask the first person in the line for the name until you have reached the line for the letter you are looking for. Then just go through this line until you have found the right person!

Say you are looking for Michael. People shuffle around and slowly form into lines. You start asking the first line: Anna… No. Next line: Eric… No. Next: Maria… Got the right line! Martin… Mary… Michael, gotcha!

In the worst case finding the right line takes 26 steps (one for every letter in the alphabet) and then following the line should not take too long either, unless all students have the same first letter which is unlikely.

This approach lends itself well to explain some of the concepts of the Inverted Index:

* You need to do some pre-processing before you can start searching, this takes a while. However, this will pay off with a much faster search.
* For a small number of students = documents this is probably not necessary and it is more effective to just look through all documents, akin to Unix’ grep.
* During pre-processing documents are parsed (picking the first letter of the name in this case) and then added to a line or bucket depending on the parsed criteria.
* You need to put some thought in the pre-processing to get it right. Which line is right for student whose names do not start with letters in the ASCII set, such as Ølaf. Do they go into the O lane or Ø, ie. do you do ASCII folding? This would reduce the number of lines but make the lines longer.
* Sorting the lines alphabetically makes it easier to find the right line (in software the lines would be hashed for faster lookup but this is hard to do in real life).
* Once you have identified the right line finding the requested document is easy since the line is relatively small.

Hope you like it!