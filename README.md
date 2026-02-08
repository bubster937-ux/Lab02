# Lab02

- Name: Andre Bond
- Email: bond.57@wright.edu

Instructions for this lab: https://pattonsgirl.github.io/CEG2350/Labs/Lab02/Instructions.html

## Part 1 Answers

Full / absolute path to your private key file: 
  /home/andre/Downloads/ceg2350-aws-vm.pem 


Command to SSH to AWS instance:
```
ssh -i Ceg2350-aws-vm.pem ubuntu@34.194.193.153
```

## Part 2 Answers

1. `chmod u+r bubbles.txt`
    - Means: It Adds read permission (r) for the file owner (u) on bubbles.txt. The owner can now open/read the file contents.
    - Assessment: very useful because It gives the owner appropriate access without granting unnecessary write/execute permissions or opening access to other users.
2. `chmod u=rw,g-w,o-x banana.cabana`
    - Means: It Sets the owner’s permissions exactly to read/write (u=rw). Removes write permission from the group (g-w). Removes execute permission from others (o-x). This reduces the ability of other users to modify or run the file.
    - Assessment: useful because It follows least privilege by ensuring only the owner can edit the file while limiting group/others from unsafe permissions.
3. `chmod a=w snow.md`
    - Means: It Sets permissions for all users (a) to write-only (w) on snow.md. Owner, group, and others can write to it but cannot read or execute it.
    - Assessment: not all that useful as it is insecure and anyone can edit the file, and it’s impractical because even the owner cannot read the contents. A markdown file should be readable.
4. `chmod 751 program`
    - Means: Means: It Sets numeric permissions on program:

Owner: 7 = read/write/execute (rwx), Group: 5 = read/execute (r-x), Others: 1 = execute only (--x)
    - Assessment: id say its ok to use but just be mindful of that fact that if you intentionally want others to execute the program its fine but giving “others” execute access can be very risky.
5. `chmod -R ug+w share`
    - Means: (-R) will add write permission (+w) is for the owner (u) and group (g) is to share and everything inside it.
    - Assessment: honestly 50/50 because its Useful for shared folders, but -R can unintentionally make many files group-writable.
## Part 3 Answers

1. Command to create new user: sudo adduser (Abond)
2. Path to new user's home directory:  /home/Abond
3. Evaluate if `ubuntu` can add files to new user's home directory: no it cannot /home/Abond is owned by Abond so they have to have the write permission
4. Command to switch to new user: su - Abond
5. Command(s) to go to new user's home directory: pwd,cd ~
6. Evaluate if new user can add files to user's home directory: yes Abond owns /home/Abond so they have write permission
7. Command to return to `ubuntu` user: exit 
8. Command to return to `ubuntu` home directory: cd ~

## Part 4 Answers

1. Command(s) to create group Abondd `squad` and add members: sudo addgroup squad
2. Command(s) to add `ubuntu` & user to group `squad`:  sudo usermod -aG squad ubuntu, sudo usermod -aG squad Abond
3. Command(s) to allow `squad` to view the `ubuntu` user's home directory contents: sudo chgrp squad /home/ubuntu, chmod 750 /home/ubuntu 
4. Command(s) to modify `share` to have group ownership of `squad`: mkdir -p /home/ubuntu/share, sudo chgrp -R squad /home/ubuntu/share, chmod -R 770 /home/ubuntu/share
5. Describe your tests and commands with the user account: su - Abond, ls /home/ubuntu, ls /home/ubuntu/share, touch /home/ubuntu/share/bob-test.txt you're switching to Abond and testing the access
6. Describe the full set of permissions / settings that enable the user to make edits: Abond is a member of squad group, /home/ubuntu means Abond can access folder paths and share is group owned by squad

## Part 5 Answers

For each, write the command used or answer the question posed.

1. Command(s) to make file using `sudo`: sudo touch hi.txt
2. Command(s) to make file with `root`: sudo su, touch/home/ubuntu/hellothere.txt, exit
3. Describe / compare ownership and permissions of files: ls -l hi.txt hellothere.txt
4. Which account can do what actions? (Type Y or N in columns)

Contents inside of `share`
| Account   | Can View  | Can Edit  | Can Change Permissions    |
| ---       | ---       | ---       | ---                       |
| `root`    |     Y      |     Y      |        Y                   |
| `ubuntu`  |      Y     |     Y      |     Y                      |
| `BOB`     |     Y      |      Y     |         N                  |

`madewithsudo.txt`
| Account   | Can View  | Can Edit  | Can Change Permissions    |
| ---       | ---       | ---       | ---                       |
| `root`    |     Y      |      Y     |           Y                |
| `ubuntu`  |      N     |     N      |            N               |
| `BOB`     |       N    |    N       |          N                 |

5. Command(s) to modify permissions: sudo chown ubuntu: squad abond14.txt, chmod 660 abond14.txt
6. How to give user account `sudo`: sudo usermod -aG sudo Abond


## Part 6 - Citations / Resources
i used a website called chmodcommand.com and superuser.com for part 2 question 4 & linuxize for 5
I used google for part 3 questions 7&8 and part 4 questions 1-4 & 6
google as well for part 5 question 1.

## Citations

To add citations, provide the site and a summary of what it assisted you with.  If generative AI was used, include which generative AI system was used and what prompt(s) you fed it.
   `chmod 751 program`: https://superuser.com/questions/245981/chmod-755-and-751 
