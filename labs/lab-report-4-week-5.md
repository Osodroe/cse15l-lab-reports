# Week 5 – Commands

## Example 1 - "grep -l"

Using grep is a great way to quickly find certain text from a list of files. Though, sometimes that list can be very large which can fill up the terminal and make it difficult to read. So, thats where -l comes in, allowing us to only print matching file names onto the terminal. 

![-l Example 1](/cse15l-lab-reports/labs/images/lab-4/-lExample1.png)

Here it is used to find any file in the ./terminal directory that contains the word lost. We don't get the context that the word is found in, but we now have a list of files that use that word that we can read through on our own or grep to the specific file to get more context. 

![-l Example 2](/cse15l-lab-reports/labs/images/lab-4/-lExample2.png)

Here we have a similar list of files, in this case we specified a list so we only got topics related to biology. This is where the usefulness of -l is best shown, as we have easily isolated a list of research papers that contain information about plants in some way. While it is more of a feature of grep, it's -l that really allows such a legible list to be created.

![-l Example 3](/cse15l-lab-reports/labs/images/lab-4/-lExample3.png)

Much like example 1, we can search through more than just one file at a time. In this case, we completely narrowed down 6 folders into just 2 results. Though since the output wouldn't be too crowded since there are so few examples, it still creates a much easier output to work with. Especially since, "tax rates" appears several times in these files which would results in a lot of extra text.

## Example 2 - "grep -r"

Searching recursively is a super useful process that is usually done by providing grep with a pattern that refers to specific files. However, what if we don't know how deep we are going or we simply don't want to worry about providing a correct pattern, we can use -r to make grep search recursively on its own.

![-r Example 1](/cse15l-lab-reports/labs/images/lab-4/-rExample1.png)

What is most interesting about this example is how that even though you did not provide grep with anything it recursively searched the working directory. So, if you just need everything within the working dir4ectory than this simple three word command can output everything quickly.

![-r Example 2](/cse15l-lab-reports/labs/images/lab-4/-rExample2.png)

What we have here is a recursive list of every file in /terminal, which could be achieved with find, however in this case would easily alter the arguments to search for specific words to narrow down the list. This is also more of an interaction with -l, which gets rid of example lines of the text and only outputs the file name. 

![-r Example 3](/cse15l-lab-reports/labs/images/lab-4/-rExample3.png)

Once again, this is just demonstrating how using -r can simplify the the the command since you don't have to create any kind of pattern or specify every file in the directory. Since you don't need to provide much, this also means you can easily search a directory and all subdirectories without even needing to know how many there are. 

## Example 3 - "grep --exclude=GLOB"

To simplify an output even further, we can simply choose to exclude certain files that match a pattern with --exclude. Simply replace GLOB with with the suffic of the files that you do not want grep to search through and they will never be touched.

![-exclude Example 1](/cse15l-lab-reports/labs/images/lab-4/-excludeExample1.png)

The first file that should have been read in /government should have been Comments_on_semiannual.txt. However, we specifically stated that any file that starts with Comment should not be read. It isn't the most useful if you are targeting a single file, but it shows that it is possible to pick and choose what files are read beyond just their directories.

![-exclude Example 2](/cse15l-lab-reports/labs/images/lab-4/-excludeExample2.png)

We know that ./plos is full of files that start with journal, but we don't want to see any of those. By telling grep to ignore anything that starts with journal, we can easily skip over the various files that are named with journal. This drastically reduces the output size and helps only gather information we know we need. 

![-exclude Example 3](/cse15l-lab-reports/labs/images/lab-4/-excludeExample3.png)

Now we can take it even further, we don't have to pick just one pattern to exclude. We have in this example a list of patterns we do not want read. In this case, since we are searching recursively, these are excluded from all files in /technical, which allows for a wide spread filter to use on any search necessary. 