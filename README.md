<font face="Corbel" size=4>
# Chatroom   
Author: LuCima   
Email:  <houlu@lucima.cn>  

A free chatroom for CLI by Python

This is a chatroom software that can run in CLI in Linux. Users can firstly run chat\_server.py. Then, multi-clients can be started and chat with each other. 

### [Change logs]  

[Aug.  30. 2016] Basic functions implemented.  
[Sept. 01. 2016] Add group function  
[Sept. 03. 2016] Change all data format into JSON  
[Sept. 08. 2016] Add (1)change group name; (2)leave group; (3)change client name; (4)bug fix.  
[Sept. 21. 2016] Use Markdown to build the README file.  
[Sept. 22. 2016] Re-design the communication protocol.  
[Oct.  03. 2016] Start to add games in chatroom.  
[Nov.  07. 2016] Finish adding chess games in chatroom.  

### [Interaction process]  

1. Connect to server
2. Client.py start two threads, one for sending and the other for receiving
3. Set client name, command: 'SN:\<name\>', server return 'Success' or 'Failure'
4. Client can get an online list from server by command: 'OL?'
5. Server returns an online list which shows all the current users, format: 'Online:\<name1\>:\<name2\>...'
6. Client can send messages to any user they want, format: '\<name\>:\<msg\>', e.g., 'Mary: hello'
7. Client can change their name by command: 'CN:\<new\_name\>'. 
8. Client can send file to any user: '\<name\>:FILE:\<filename\>'. 

### [Group talk]

1. Any client can create a non-existing group by typing: 'CG:\<name\>'
2. By command 'GP?', clients can check the existing group, format: 'Group:\<group1\>:\<group2\>...'
3. 'EG:\<name\>' enables a client to enter the group with \<name>
4. Client can send messages to a group just as to common users: '\<group\>:\<msg\>', all clients that have entered the group can receive the msg. 
5. Group clients can change the group name by command: 'CP:\<old\_name\>:\<new\_name\>'.
6. Clients in a group can leave the group by command: 'QG:\<group\>'.

### [Black list]

1. Client can move some one to its blacklist so that it will not hear from the one, command: 'BL:\<name1\>:\<name2\>...'.
2. By simply typing: 'BL?', clients can check their black lists.  

### [Gaming]

1. Clients can play games with others by command: '\<name\>:PLAY:\<game_name\>'.
2. When your friend agrees to play, he/she will take the first step.
3. For line-in-a-row games, you can send your move by command: '\<name\>:<\game\_name\>:\<move\>'. For example, if you 
    want to put a chess piece at place (A, 9) when plays Gomoku with Mary, just typing: `mary:Gomoku:A, 9`.  
4. Clients can check current state of the game by command: '\<name\>:<\game\_name\>'.  
5. Current game list:
    - Gomoku
    - TicTacToe
    - FourInARow
    - Customized line-in-a-row game

### [Voting]

_(TODO)_

--- 

## JSON Structure:
```
Client:
{  
    Command: <command>,  
    Value: <val>,  
}  
```
Command includes:    
+	OL?                         	    : Get current online list  
+	GP?                         		: Get current chatting group  
+	BL?                         		: Get black list    
+   GM?                                 : Get game list
+   SN:\<name\>                         : Rename  
+	CG:\<group\_name\>                  : Create a new group  
+	EG:\<group\_name\>                  : Enter a group  
+	CN:\<name\>                  		: Change name  
+	QG:\<group\_name\>                  : Quit a group  
+	CP:\<old\_group\>:\<new\_group\>    : Change group name  
+	BL:\<name1\>:\<name2\>...           : Move name1... to the black list  
+   MG:\<msg in JSON\>     
    -   dst:\<name\>    : Destination name   
    -   flt:\<type\>    : File type if a file is delivered  
    -   gme:\<game\>    : Game name if you want to play a game
    -   msg:\<message\> : Message or file   
    -   tim:\<time\>    : Time  

_All Commands are case insensitive_  
```
Server:
{  
    Command: <command>,  
    Value: <val>,  
}  
```
Command includes:  
+	Online      : Online list    
+	Group       : Group list  
+   Black       : Black list
+	Resp        : Response of some command (Success or Failure)  
+	Message     : Message in JSON:  
    -   src:\<name\>    : Source  
    -   dst:\<name\>    : Destination  
    -   flt:\<type\>    : File type if a file is delivered  
    -   gme:\<game\>    : Game name if you want to play a game
    -   msg:\<message\> : Message or file  
    -   tim:\<time\>    : Time

</font>
