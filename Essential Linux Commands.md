## Essential Linux Commands

## Files And Directories

- mkdir : to create an empty directory
- rmdir : to remove an empty directory
- ls : list files 
- cd : change directory 
- mv : move or rename file
- cp : to copy file
- touch : make a file 
- grep search for a file 
- pwd : print working directory
- rm : remove file
- cat : display file content
- chmod : change file permission 
- echo : to print to the screen or to a file 

### Examples

Create a folder with the name 'Linux' and navigate to that folder and create 3 files, named file1, file2, file3

```bash
mkdir Linux 
```

This command above will create the emoty directory named Linux now let's navigate to this directory and create the needed files 

```bash
cd Linux
```

Now let's create the needed files

```bash
touch file1.txt file2.txt file3.txt 
```

Let's create another folder so we can move some files to it , create a folder called  MyFiles

> Hint: Use mkdir

Now let's move file1.txt to the MyFiles folder

```bash
mv file1.txt MyFiles
```

Let's navigate to MyFiles and add some data to the file1.txt

> Hint: Use cd

Now let's add this text "I love linux " to the file 

```bash
echo "I Love Linux" >> file1.txt
```

Notice the >> is to redirect the data to the file1.txt. Now let's actually test it the data is added to the file 

```bash
cat file1.txt
```

Now we should see the data added to the file printed in out terminal

Let's now make a copy of file1.txt and add some lext to it

```bash
cp file1.txt file2.txt
```

add this text "Linux is cool" to file2.txt

> Hint: Use echo >>  

Now let's move file1.txt back to Linux folder
First let's navigate back to the folder using cd like this

```bash
cd ..
```

Using cd with .. will take us back one folder backward, now let's get the working directory so we can copy the file back to it

```bash
pwd
```

Now copy the output of pwd and go back to the MyFiles folder using cd MyFiles
Now let's rename file1.txt and move it back to Linux folder

```bash
mv file1.txt file01.txt
```

We also use mv to rebame files, let's now move it back

```bash
mv file1.txt /Users/bounasrnour/Linux
```

Now let's delete file2.txt 

```bash
rm file2.txt
```

Let's go back to Linux folder with cd ..
Now let's assume we have a lot of files and we want to search for a specific file let's say files with .txt at the end

````bash
ls | grep .txt
````

using the | will let us chain commands together, like we did, the ls command will list all files and the grep command will search for files with only .txt extension this the output will be a list of files with the .txt extension

Now let's cover the last command chmod, sometimes we want to change the permissions to execute files or prevent some users from executing or reading, writing files this can be done with the chmod command 
The chmod has 3 groups owner, group, other  let's see how it works

This can be read only by owner 

```bash
chmod 400 file1.txt 
```

Read only by group

```bash
chmod 040 file1.txt
```

Write by other

```bash	
chmod 002 file1.txt
```

Write by owner

```bash
chmod 200 file1.txt
```

Execute file by owner

```bash
chmod 100 file1.txt
```

If you want to give read, write or execute you can add the numbers together as follow
For read, write by owner

```bash
chmod 600 file1.txt
```

For read, write and execute by owner

```bash
chmod 700 file1.txt
```

Allow read, write, execute by everyone 

```bash
chmod 777 file1.txt
```



## Summary

In this article, I covered the most essential linux commands, if you have any question or you want to know more about something related to some specific command feel free to comment below.



