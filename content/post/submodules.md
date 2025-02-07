+++
title = "Why Git Submodules Are Kinda Lame"
date = "2025-02-06"
author = "Dan"
cover = "imgs/submodule1.png"
description = "Or rather - what git submodule is meant to provide is too often overruled by what people want out of git submodule."
+++
# Why Git Submodules Are Kinda Lame

Funny story: when I was still a junior I had a tendency to ask questions to my mentors a lot and some of them 
went like: "hey Mentor, why don't we use git submodule for this instead of copying a whole repository into 
our codebase?"

Oftentimes, he would politely answer or send me a resource where I could read more later. This question must 
have broken him though. 

He sent me a gif over slack, this one actually:

{{<figure src="https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExbmZvbW5vd3I4bnB4c2VjdDA0dXhjb2I4cGpwa3RkZzVlcWVueWZvZyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/8vUEXZA2me7vnuUvrs/giphy.gif" 
caption=""
alt="michael scott saying no"
>}}

I figured he was sick of my questions and just went with the static library decision he was going for. It was 
so long ago now that I don't remember if the submodules were going to be updated with new commits or if they 
were always going to be left alone. We had a lot of both kinds of repos at my old company. Still, to me it 
seemed like an reaction one would only have if they ran into huge trouble with the tool in the past. Or if I 
was annoying them too much. Anyways, I came to agree with him over time about submodules - avoid them if you 
can.

But why?

Really, because it adds complexity. You need to remember to `git submodule update` besides the usual clone 
and checkout when you're beginning a project. That can cause unexpected behavior for other devs if you didn't 
take care to document setup, which you didn't do. Or if you're making changes in the submodule you'll need to 
remember to push those to the submodule and to the repo you're 
actually working in. And then once those changes are made, switching branches is now a pain in the ass. This 
can make basic things like a MR a lot harder to manage, and if you didn't need things like updating a git repo 
acting as a module in your codebase then why go through the effort?

A more compelling reason to avoid git submodule is because a package manager can probably do what you want 
better - storing a reference to a specific version of another package. Treating git like a package manager can 
also lead to bugs that aren't really there - the submodule not being updated when you expected it to for 
example. It violates the SRP by being both a git repo tracking changes and a PM at the same time.

So git submodule is left with a very narrow use case: a PM when you want to also on-the-fly update the package. 
But not too often though. You can easily separate these concerns in my view, so I avoid git submodule in serious 
projects when I can.

I went ahead and used it anyways in this website for the Hugo theme lol shoutout to panr. It's not like I'm 
working on this site with anyone else!