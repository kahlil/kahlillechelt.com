---
date: 2018-11-21T09:01:05+01:00
title: 'Vimming in the Squasher: How to Squash your Commits with VIM'
---

Whenever I use `git rebase -i` to squash commits, Git opens the squasher (that’s how I just named the text view for the
interactive rebase) in VIM.

My knowledge of vimming is not very great so I used to just type `i` and then inch around with the arrow keys and delete
character by character in order to delete the word “pick” a bunch of times and then type “squash” a bunch of time.

Of course that was incredibly annoying, so
[I finally looked up](https://coderwall.com/p/d6gifw/use-vim-visual-blocks-to-squash-multiple-git-commits) how to vim in
the squasher and it is glorious. So here is how you do it:

First, move to the line with the first commit you want to squash, which is typically the second one.

Then, enter into something called _visual block mode_ (WTF?! What does that even mean?) by hitting `ctrl` + `V`.
Something magical happens: when you move the curser it blocks out every character you move over with white and if you
move down it will cover as many characters you covered in the line above. It looks like blocks. So I guess that's where
the "visual block" comes in 😅.

Select all the rows you wish to squash while visually blocking out the word "pick".

Now, more magic: hit `C` and type the word "squash", after that hit `esc` and see the word "squash" applied in all
places that were "visually blocked out".

If you only could exit VIM at this point, you would actually successfully squash all these commits. A boy can dream,
right?
