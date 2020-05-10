## Submission for Unit 6 Advanced Bash Homework

Create a secret user named `sysd`. Make sure this user doesn't have a home folder created.
- `useradd sysd `

Give your secret user a password.
- `passwd sysd`
                toor  
                toor

Give your secret user a system UID < 1000.
- `usermod -u 700 sysd`

Give your secret user the same GID
- `groupmod -g 300 sysd`

Give your secret user full sudo access without the need for a password.
- `visudo`

editing sudo file and adding

sysd    ALL=(ALL:ALL) NOPASSWD:ALL  

under root entry..

Test that sudo access works without your password

```bash
Your BASH commands go here

sudo -l

#check!


## Allow ssh access over port 2222.

```bash
ls /etc/ssh/sshd_config
nano /etc/ssh/sshd_config

systemctl restart ssh


```

Note the IP address of this system:
- `ifconfig `
    '172.17.14.199'
Exit the root accout.
- `exit `
SSH to the machine using your sysd account and port 2222
- `YOUR SOLUTION COMMAND HERE`
Use sudo to switch to the root user
- `YOUR SOLUTION COMMAND HERE`

### Create a backdoor with socat
- Install socat
  - `YOUR SOLUTION COMMAND HERE`
- Run Socat command in the background
  - `YOUR SOLUTION COMMAND HERE`
- Explain each part of the `socat` command:
  - `YOUR SOLUTION COMMAND HERE`
  - `YOUR SOLUTION COMMAND HERE`
  - `YOUR SOLUTION COMMAND HERE`
- Exit the SSH session
  - `YOUR SOLUTION COMMAND HERE`
- Test socat connection from the Ubuntu machine:
  - `YOUR SOLUTION COMMAND HERE`
- Close the `socat` connection.
  - `YOUR SOLUTION COMMAND HERE`

## Crack _all_ the passwords
Ssh back to the system using your sysd account
- `YOUR SOLUTION COMMAND HERE`
- Use John to crack the entire /etc/shadow file
    - `YOUR SOLUTION COMMAND HERE`

## Cover your tracks
- Use socat and a for loop to clear all system logs.
- `YOUR SOLUTION COMMAND HERE`
