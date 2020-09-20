# Python cmd prompt

Ref : [https://pymotw.com/2/cmd/](https://pymotw.com/2/cmd/)

* Goals
  * command = "TiMe" : This will print sometime
  * command = "NaMe" : This will print some name.
  * command = anything other than the above 2 commands : Then print a message to enter valid command.

```text
import cmd

class exploit(cmd.Cmd):
    prompt = "CMD > "

    def default(self, line):
        print("Please enter a valid command")
    
    def do_TiMe(self, line):
        print("You have entered" + line + " and time is 12:30pm")
        
    def do_NaMe(self, line):
        print("You have entered" + line + " and name is John Doe")
        
exploit().cmdloop()
```

