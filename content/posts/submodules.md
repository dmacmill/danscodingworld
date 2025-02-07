+++
title = "Why Git Submodules Are Kinda Lame"
date = "2025-02-06"
author = "Dan"
cover = "imgs/submodule1.png"
description = "Or rather - what git submodule is meant to provide is too often overruled by what people want out of git submodule."
+++
# Why Git Submodules Are Kinda Lame

First, a funny story. I was a mid-level dev that was getting more confident in things like tooling, and wanted 
to impress people by asking probing questions. I asked one when working with someone who was copying a repo as 
a whole static library for a backend app we were writing. 

"Hey, why don't we use git submodule for this instead of copying a whole repository into our codebase?"

Oftentimes, he would politely answer or send me a resource where I could read more later. This question must 
have broken him though. 

He sent me a gif over slack, this one actually:

{{<figure src="https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExbmZvbW5vd3I4bnB4c2VjdDA0dXhjb2I4cGpwa3RkZzVlcWVueWZvZyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/8vUEXZA2me7vnuUvrs/giphy.gif" 
caption=""
alt="michael scott saying no"
>}}

I figured I was being annoying and so we just went with the static library decision he was going for. And 
for the record, I think I was being a little annoying. He normally wasn't like that. It was 
so long ago now that I don't remember if the submodules were going to be updated with new commits or if they 
were always going to be left alone. We had a lot of both kinds of repos at my old company. Still, to me it 
seemed like an reaction one would only have if they ran into huge trouble with the tool in the past. Or if I 
was annoying them too much. Anyways, I came to agree with him over time about submodules - avoid them if you 
can.

But why?


Really, because if your use case changes from "I just need this never changing package" to "I would like to 
change this package a whole lot, make a lot of commits to it" then you're better off with those static 
libraries. They can change or stay the same if you want them to. They're flexible, submodules aren't.

I mean, you can make changes with a commit, but that just opens another can of worms. You need to remember 
to `git submodule update` for other devs working in the same branch. If you don't, switching branches, 
merging, MRs, all become a pain in the ass, etc. If you didn't need things like updating a git repo 
acting as a module in your codebase then why go through the effort?

Plus, it can be a source for bugs when `git submodule update` is called and you didn't expect changes to be 
breaking, become breaking anyways. Like for a repo that wasn't meant to change often, but did because whatever 
changed was out of your hands.

Another reason to avoid git submodule is because a package manager can probably do what you want 
better - which is storing a reference to a specific version of another package. Treating git like a PM when it 
is designed so that users can make changes to the codebase feels like a violation of the 
Single Responsibility Principal. Only violating the SRP in this case can be a nusiance at best, and a source 
for bugs at worst.

I went ahead and used it anyways in this website for the Hugo theme to give it another shot, and sure enough 
it was unnecessary for the thing I needed, which was just a working static version of a Hugo theme. I could 
have easily just copied the files I needed into the themes folder and reduced complexity. Lucky for me, I 
don't plan to call the update command or make commits or do anything weird. But if I changed my mind, I might 
be in for a world of pain!

So if I need to make changes to a git repository, I make changes to them elsewhere or in the static library 
where I need those changes and nowhere else. That way I can better tailor the library to suit my projects needs. 
I can see why one would still want to use git submodule, if their needs from PM to place to make some commits 
change mid-project for example. But I feel like that's a very narrow use-case and I - for one - can separate 
those concerns.
