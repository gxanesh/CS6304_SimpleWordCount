# SimpleWordCount

### General Information:

* Operating System:         Mac -> Microsoft Remote Desktop, Windows -> Default Remote Desktop, Ubuntu -> Remmina
* Machine:                  cs6304-<mst_username>-01.class.mst.edu
* User:                     <mst_username>
* Default Password:         <mst_password>

### Importing Project:
* Open “Eclipse”, Right-Click on the “Package Explorer” window, and click import.
* Select “Git”-> “Projects from Git” and click “Next”.
* Select “Clone URI” and click “Next”.
* Copy and Paste “https://github.com/gxanesh/CS6304_SimpleWordCount” in the “URI” textbox, and click “Next”.
* Select the "master" branch on Branch Selection and Click "Next"
* For Local Destination, Keep the Directory Field as it is: "/home/<your_SSO>/git/CS6304_SimpleWordCount" and Click "Next"
* Choose “Import existing project”, Click "Next" then Click “Finish”.

### Referencing libraries:
* Right-click on the project and select “build path”-> “configure build path” ->” Libraries”->” Add External Jars”.
* Go to "home" -> "git" -> "SimpleWordCount" -> "lib" and select all jars and click "Open"-> Click "Apply and Close".

### Input file:
* Open folder "file", you will see the input file named "WordCount.txt"

### Output jar:
* Right-click on the project and select "Export".
* Choose type "Java" -> "Jar file" and click "next".
* Select the export destination as "home" -> "git" -> "SimpleWordCount" -> "bin" -> Set Name "output.jar" and click "Save" then Click "Finish".

### Hadoop Commands:
```
hadoop fs -mkdir -p InputFolder                                      //to create a new input folder
hadoop fs -copyFromLocal <input file> InputFolder                  //to copy a file from the local directory to the Hadoop environment
Eg:hadoop fs -copyFromLocal '/home/gs37r/git/CS6304_SimpleWordCount/file/WordCount.txt'  InputFolder
hadoop fs -ls InputFolder                                          //to see the files inside "InputFolder"
hadoop jar <jar file name> <class name> InputFolder OutputFolder   //running MapReduce operation
Eg: hadoop jar '/home/gs37r/git/CS6304_SimpleWordCount/bin/output.jar'  WordCount 'InputFolder/WordCount.txt' OutputFolder 
hadoop fs -ls OutputFolder                                        //to see the files inside "OutputFolder"
hadoop fs -cat OutputFolder/part-r-00000                          //to see the content inside "OutputFolder/part-r-00000" file
hadoop fs -rm -r OutputFolder                                     //to remove the "OutputFolder" directory and all its files
```

- remove OutputFolder before generating the next results.
- Remove/clean InputFolder if you want to use a different file for input.


### Common Errors:
Error 1: mkdir: Call From cs6304-gs37r-01/127.0.1.1 to localhost:9000 failed on connection exception: java.net.ConnectException: Connection refused  
Explanation and Fix: In general this error comes if you are running hadoop first time on your VM after a reset. The below commands will fix it.
```
stop-all.sh
hadoop namenode -format
start-all.sh
```
You can use the below command to check if namenode, datanode and nodemanager are running.
```
jps

```

Error 2: mkdir: `hdfs://localhost:9000/user/<username>': No such file or directory  
Explanation and Fix: The error comes when there is no directory /user and /user/<username> in hdfs and you are trying to create a folder using "hadoop fs -mkdir InputFolder ".   
The below command will create the directory structure if required and solve the problem.
```
hdfs dfs -mkdir -p InputFolder
```

Warning 1: WARN util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable  
Fix: You can ignore this warning.


