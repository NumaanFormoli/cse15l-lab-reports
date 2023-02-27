# Lab Report 3: Experimenting with grep command
---

1. Match regular expression in files using -r and -l


    ```
    numaanformoli@Numaans-MacBook-Air written_2 % grep -r -l "t.*pw" non-fiction/

    non-fiction//OUP/Berk/ch1.txt
    non-fiction//OUP/Kauffman/ch3.txt
    non-fiction//OUP/Kauffman/ch1.txt
    non-fiction//OUP/Kauffman/ch7.txt
    non-fiction//OUP/Kauffman/ch6.txt
    non-fiction//OUP/Kauffman/ch8.txt
    non-fiction//OUP/Fletcher/ch9.txt
    non-fiction//OUP/Castro/chA.txt
    non-fiction//OUP/Castro/chM.txt
    non-fiction//OUP/Castro/chZ.txt

    ```
    ```
    numaanformoli@Numaans-MacBook-Air written_2 % grep -r -l "stops*" non-fiction/         

    non-fiction//OUP/Berk/ch2.txt
    non-fiction//OUP/Berk/ch1.txt
    non-fiction//OUP/Berk/CH4.txt
    non-fiction//OUP/Berk/ch7.txt
    non-fiction//OUP/Abernathy/ch2.txt
    non-fiction//OUP/Abernathy/ch9.txt
    non-fiction//OUP/Rybczynski/ch2.txt
    non-fiction//OUP/Kauffman/ch3.txt
    non-fiction//OUP/Kauffman/ch7.txt
    non-fiction//OUP/Kauffman/ch8.txt
    non-fiction//OUP/Kauffman/ch9.txt
    non-fiction//OUP/Kauffman/ch10.txt
    non-fiction//OUP/Fletcher/ch2.txt
    non-fiction//OUP/Fletcher/ch1.txt
    non-fiction//OUP/Castro/chM.txt
    ```
    - In this example, I use the regex to search text files in the non-fiction directory that has a pattern that starts with t and ends with pw. I use the -r to search through the directory recursively and -l to only list the file name. This is useful if you want to search a directory for a certain pattern, say an email address, but don't want to grep each txt file. The * means that the preceding character will be matched zero or more times.
    - [Source](https://www.thegeekstuff.com/2009/03/15-practical-unix-grep-command-examples/)
 
 
2. Invert match using grep -v

    ```
    numaanformoli@Numaans-MacBook-Air travel_guides % grep -v "a" berlitz1/HandRHawaii.txt
            410 rooms.
            rooms.
            402 rooms.
            <www.outrigger.com>. This 17-story tower, perched on one of the
            66 rooms.
            pools. 806 rooms.
            rooms.
            (808) 879-8763; <www.westin.com>. The most southwesterly of
            immense koi pools. 310 rooms.
            rooms.
            grounds. 1,240 rooms.
            350 rooms.
            with dozens of turtles. 545 rooms.
            60 rooms.
    ```
    ```
    numaanformoli@Numaans-MacBook-Air travel_guides % grep -v "a" berlitz1/HistoryIsrael.txt    
            A Brief History
            remembered for his wisdom, for the construction of the First Temple,
            Jewish culture nonetheless survived the second destruction of the
            respectively.
            positions in Beirut. They forced the PLO out, but without much support
            people.
    ```
    - In this example, I use the command option -v which does an invert match meaning it returns the lines that do not contain that pattern. This would be useful in searching for a specific file that does not have a particular pattern.
    - [Source](https://www.thegeekstuff.com/2009/03/15-practical-unix-grep-command-examples/)


3. Counting the number of matches using grep -c

    ```
    numaanformoli@Numaans-MacBook-Air travel_guides % grep -c "of" berlitz2/Algarve-History.txt
    30
    ```
    ```
    numaanformoli@Numaans-MacBook-Air travel_guides % grep -c -r "No" berlitz2/Athens-WhatToDo.txt 
    berlitz2/Athens-WhatToDo.txt:1
    ```
    - The -c command option counts the number of lines with matches. This can be useful if you want to know the frequency of some word within a text file.
    - [Source](https://www.thegeekstuff.com/2009/03/15-practical-unix-grep-command-examples/)


4. Case insensitive search using grep -i

    ```
    numaanformoli@Numaans-MacBook-Air Fletcher % grep -i -l "hi" *.txt  
    ch1.txt
    ch10.txt
    ch2.txt
    ch5.txt
    ch6.txt
    ch9.txt
    ```

    ```
    numaanformoli@Numaans-MacBook-Air written_2 % grep -i -l -r "why" non-fiction 
    non-fiction/OUP/Berk/ch2.txt
    non-fiction/OUP/Berk/ch1.txt
    non-fiction/OUP/Berk/CH4.txt
    non-fiction/OUP/Berk/ch7.txt
    non-fiction/OUP/Abernathy/ch3.txt
    non-fiction/OUP/Abernathy/ch1.txt
    non-fiction/OUP/Abernathy/ch7.txt
    non-fiction/OUP/Abernathy/ch8.txt
    non-fiction/OUP/Abernathy/ch15.txt
    non-fiction/OUP/Rybczynski/ch2.txt
    non-fiction/OUP/Rybczynski/ch3.txt
    non-fiction/OUP/Rybczynski/ch1.txt
    non-fiction/OUP/Kauffman/ch3.txt
    non-fiction/OUP/Kauffman/ch1.txt
    non-fiction/OUP/Kauffman/ch4.txt
    non-fiction/OUP/Kauffman/ch5.txt
    non-fiction/OUP/Kauffman/ch7.txt
    non-fiction/OUP/Kauffman/ch6.txt
    non-fiction/OUP/Kauffman/ch8.txt
    non-fiction/OUP/Kauffman/ch9.txt
    non-fiction/OUP/Kauffman/ch10.txt
    non-fiction/OUP/Fletcher/ch2.txt
    non-fiction/OUP/Fletcher/ch1.txt
    non-fiction/OUP/Fletcher/ch5.txt
    non-fiction/OUP/Fletcher/ch6.txt
    non-fiction/OUP/Fletcher/ch9.txt
    non-fiction/OUP/Fletcher/ch10.txt
    non-fiction/OUP/Castro/chR.txt
    non-fiction/OUP/Castro/chM.txt
    non-fiction/OUP/Castro/chN.txt
    ```
    - This option -i looks for the pattern without case sensitivity. It is useful when looking for a word that can appear in a text in uppercase or lowercase.
    - [Source](https://linuxhandbook.com/grep-command-examples/)
