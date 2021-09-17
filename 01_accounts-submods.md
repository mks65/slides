name: main

### .aim[NeXTCS: Drawing in Processing.]

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
### Drawing functions

* `rect(x, y, width, height)`
  - Draw a rectangle starting at `(x, y)` with the given dimensions.
