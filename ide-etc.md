## MAC
### [MAC git can not auto complete](https://apple.stackexchange.com/questions/55875/git-auto-complete-for-branches-at-the-command-line)
ok, so I needed the git autocompletion script.

I got that from this url:

curl https://raw.githubusercontent.com/git/git/master/contrib/completion/git-completion.bash -o ~/.git-completion.bash

No need to worry about what directory you're in when you run this as your home directory(~) is used with the target.

Then I added to my ~/.bash_profile file the following 'execute if it exists' code:
```
if [ -f ~/.git-completion.bash ]; then
  . ~/.git-completion.bash
fi
```
Update: I'm making these bits of code more concise to shrink down my .bashrc file, in this case I now use:

```
test -f ~/.git-completion.bash && . $_
```
Note: $_ means the last argument to the previous command. so . $_ means run it - "it" being .git-completion.bash in this case

This still works on both Ubuntu and OSX and on machines without the script .git-completion.bash script.

Now git **Tab** (actually it's git **Tab** **Tab** ) works like a charm!

(PS: If this doesn't work off the bat, you may need to run chmod -X ~/.git-completion.bash to give the script permission to run.)
