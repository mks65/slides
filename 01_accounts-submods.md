name: main

### .aim[Systems: Starting C & GitHub Setup]

<style></style>

<hr>

---
template: main

### Do Now: CS Account Setup!
You now have a stuycs account that will allow you to use the cs lab computers.
Account information:
* username: stuy.edu username
* password: OSIS followed by homeroom, 2 leters, lowercase

Example:
* username: dw
* password: 1234567893rr

---
template: main

### Changing CS Account Password
Your password is currently __terrible__. Once you have completed the steps on a given slide, raise your hand, and keep it raised until told otherwise.

--

1. Log into the computer in front of you.
2. Open a terminal (shortcut: ctrl-alt-t)

--
3. SSH onto the file server using the following in terminal:
   * `$ ssh 149.89.17.91`
   * You will be asked for your password, as you type, the cursor __will not move__ this is normal and desired behavior.
   * Once logged in, your terminal should display something like:
     - `username@cs-nfs:~$`
???
students WILL complain about the cursor not moving.
--
4. Change your password using the following command:
   * `$ yppasswd`
   * Follow the prompts. Once again, your cursor will not move while entering passwords.

--
5. Logout of cs-nfs (type `exit` in the terminal), log out of the computer.
6. Log back into the computer with your newly set password.

---
template: main

### Github Submodules

All work for this class will be submitted using submodules on github. Think of a submodule as a github repo inside another github repo.

  1. Each class will have a repo for assignments.
  2. Each student/group will create a totally separate repo for their work on their own gh account.
    * This should not live in the main work repo.
  3. Each student/group will clone the main work repo, and then link their own repo as a submodule.
  4. Each student/group will get rid of their local copy of the main repo.
  5. Each student/group will work on their assignment in the repo created in step 1.

---
template: main

### Submodule Setup

Follow along with these steps:

  1. Log into GitHub in a browser and create a new repository. Don't forget to include a README.md file.
  2. Clone that repo on your computer.

--
  3. __Clone the main work repo:__
     * `$ git clone git@github.com:mks65/01_start.git`
--
  4. __Change into the correct directory and add your repo as a submodule__
     - `git submodule add -b <BRANCH> <URL TO YOUR REPOSITORY> <required submodule directory name>`
