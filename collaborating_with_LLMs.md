# Collaborating with LLMs

_This is a more in depth view of how I actually work with LLMs today to get work done_

_As practices around LLMs keep changing, knowing when a piece is from becomes more important: Last edited Monday July 27th 2026_

This page is some of my writings from experimenting building interactive explainer to showcase how [Cloud Optimized Geotiff HTTP Range Requests](https://x.com/MaxLenormand/status/2077741301055795593?s=20), [H3 hexagons](https://x.com/MaxLenormand/status/2080284304496550045?s=20) or [Zarr](https://x.com/MaxLenormand/status/2079556266880315564?s=20) work. 

These projects combine together a few different things:
- Interactive elements
- Working with real data
- Educational

I use Claude Code with [Fused Render](https://github.com/fusedio/fused-render) to make these projects though think of these more of a 'how to collaborate with LLMs' set of thoughts than something specifically applied to these tools. 

### Principles

**Write up front**

LLMs have gotten great at building a lot of pieces of software you cna think of. They are also very eager to provide an opinion about what you're asking them if prompted. I do think LLMs should just be yet another tool -albeit a smart one, but a tool nonetheless- to help build something with a vision. 

I'm trying to keep myself accountable to this by:
- Writing what I want without asking for an LLM to give input the moment I feel even the smallest hint of feeling stuck
- Stepping away from the terminal and writing outside of the temptation of a quick rapid question and answer

**Iterate more**

Once I've got a good sense of what it is I want, then I fire up a bunch of agents to provide multiple different versions of what I have in mind, try different implementations, 


### Setup

Conversations about tools & gear are always the ones people go to first, it's common to think that if only I had the right tool, I too could make cool stuff. It matters less than we give it credit for. It's still fun to nerd about though, so here are the stuff I use today:

**Terminal: `cmux`**

![Multiple Claude Code sessions running in parallel](img/parallel_claude_sessions.png)

I like this because I have multiple ideas / projects going on at the same time. After trying a few things (namely multiple tabs in `iTerm2` tiled in different corerns of my screen) `cmux` is what I've stuck with. 

What I like about it:
- Legibility: I have it in split screen on my laptop and can see a good chunk of each conversation. 
- Organization: Sorting conversations in folders, giving them unique colors, etc. 
- A single app for all chats: I use the `Cmd + Shift` a ton on Macos to shift between tabs & workspaces as I often work just on a laptop. Having all Claude Code sessions in a single app is a simple way to just go to all conversations.

**Claude Code**

This is where I'm currently lacking, I still haven't tried out Codex and have extensively been using Anthropic's offering, partly because keeping up with their model is plenty of work already, partly because I started with Claude Code and habits die hard.

**Fused Render** 

I've worked as developer advocate at Fused, so I've been dog fooding the product. We're just about to release Fused Render, a framework for writing HTML + Python together for larger analytics work that's 1 click to dpeloy. It's taking Claude artefacts and putting them on steroids for larger work. This is mainly what I've been using

### Workflow

**I've never been so distracted**

It's so tempting to launch a claude code session, and immediately go do something else while the model runs. I've ended up starting 6-7 conversations all at once because of that and then ended up just jumping between session, one on a new feature,s another writing an exmaple, another organizing files locally, and yet another doing some research for a new project. This is a terrible way to work, at least for me. I end up scattered and half-assing everything. The way out of this for me has been to:

1. Write ideas out
2. Prototype multiple versions
3. Write bulk feedback for LLM
4. Iterate until happy 

I've been using Claude Code + Fused Render to create some explainers for some topics around geospatial analysis. I made ones for [Zarr](https://x.com/MaxLenormand/status/2079556266880315564?s=20), [H3 hexagon tiles](https://x.com/MaxLenormand/status/2080284304496550045?s=20) and [Cloud Optimized Geotiffs](https://x.com/MaxLenormand/status/2077741301055795593?s=20). Let's use the Zarr example as a case stufy of how I worked:

1. Writing ideas out

I start by writing down in a new text file, not in the terminal what I want to build

<img src="img/zarr_explainer_brainstorm.png" alt="Zarr brainstorm" style="width: 50%; display: block; margin: 0 auto;" />

This serves multiple purposes:
- Writing forces me to actually think about what I want. Who the target audience is, what do I want someone who goes through this explainer to walk away from, what is in & out of scope?
- Provides the LLM a better idea of what it is I'm trying to do and provide some ideas. 
- Grouding explainer in credible sources: either for what to say (i.e. content) or how to present it (UI, visual look, etc.). Especially for technical explainers, I don't want to rely just on an LLMs knowledge from training. There are a lot of well written pieces I already know about that I cna point to. These are pieces I've read myself, and have already deemed useful. I don't completely outsource this to LLMs either

2. Prototype multiple versions

LLMs have made code cheap and iteration fast. They lack good common sense and are terrible judges of the value of their own work, but I have that. So I use LLMs to try out many different ideas, implementation, kepe the best and kill the rest. 

For the Zarr explainer, I asked Fable to build 3 versions of this explainer, in different styles and with various degrees of depth. It's become so much simpler to try out ideas that might not be worth it and see how they turn out. I do recommend leaning into this hard, make mulitple versions. You have a machine that pumps out code, use it and keep homing your human judgement to ruthlessly kill all the bad ideas and only keep the good ones. It's simpler than ever to not be attached to ideas because you didn't spend weeks implementing it. 

![Zarr attempts](img/zarr_attempts.png)

I asked Claude to make multiple versions with more or less technical depths each time:

<table>
  <tr>
    <td width="33%"><img src="img/zarr_explain_A.png" alt="Less technical version" /></td>
    <td width="33%"><img src="img/zarr_explain_B.png" alt="Middle technical version" /></td>
    <td width="33%"><img src="img/zarr_explain_C.png" alt="Most technical version" /></td>
  </tr>
</table>

_Left to right: least technical to most technical. Click any of them to see the full size._

This allows me to test different approaches, see & feel how they are to interact. In this case my goal is to build an interative explainer for Zarr, the file store format. In the end I ended up taking multiple ideas from each interation into a single one and refined it into what I think is a more complete explainer

3. Write bulk feedback

When i first started working on these projects I would write all my feedback directly into the CLI and send it over to my LLM to figure out. This quickly got complicated to track (did I already mention this mis-aligned button?) so now I write my feedback for LLMs direclty in a text file, something like this:

```
### Feedback on Zarr 1 page explainer
[Link](...zarr_story_steps/explainer.html)

- [Step 2](...zarr_story_steps/explainer.html?step=2)
	- Would be great to actually show instead of a square, to scale rendering of lat / lon, i.e. rectangle and draw the contour of the world to give at least an idea this is world-wide example
- [step 3](...zarr_story_steps/explainer.html?step=3)
	- Looks visually exactly the same as step 2, hard to tell we went from full dataset to chunk apart from reading the numbers. Quick visual glance doesn't really show that 
- Step 4
	- Would be great if this was interactive, i.e. I could hover on this myself and see it update rather than it being dedicated 
```

I use a few elements to do this:
- Fused render allows to link to query params for a specific section of the page, for example:

```
https://.../my_project.html?page=intro&color=black
```

This allows me to pick & chose only specific components of the different existing versions I then ask Claude to put together into a single coherent versions, picking what I think are the best of each version.

I provide my feedback in bulk, meaning I write it all specifically as I explore what's being built:

![written feedback](/img/feedback_written.png)

4. Iterate until happy

LLMs are getting much better at one shotting complex projects, i.e. giving you a workable output given the first prompt, especially with models like Fable & Opus 5. This also has meant the work is changing every few months. At the time of writing this (July 2026), the work I find still required is:
- **Writing**: Models are still really bad at providing writing that doesn't sound all the same. I usually replace whatever text a model outputed and replace it with my own. 
- **UX / UI**: Buttons are misaligned, hover states don't make sense, these are still common things I provide feedback on the 2nd or 3rd iteraiton of a project. 
- **Consicness**: Many of these models also love talking and showing off how much they know. Even with skills like [caveman](https://github.com/JuliusBrussee/caveman) or [i-have-adhd](https://github.com/ayghri/i-have-adhd) things don't always get cut out properly. This can happen where text is too long, or a page of one of the explainers goes in way too much details, while missing the most important concepts. 

This is where I've found my work changing: I'm becoming more of a project manager, planning work out and then reviewing, providing feedback, the way an editor might also, much more than actually implementing the work itself anymore.

### Ship fast

It's all fun and games to go back & forth with Claude, polish one last thing, add one more detail, improve one more flow. But implementations are cheap so it becomes more important to validate ideas earlier. In the scope of my explainers, this means putting it out into the world, posting it on socials and seeing if anybody cares. 

If nobody even clicks on my project, who cares if one of the button's hover state looks odd? Don't get me wrong I deeply care about making things well, but I want to also make things people also care about and want to use. When everyone can buidl with Claude, it's even harder to get other people to play around with your new project, everyone's busy playing with theirs. 

Get validation quickly, from colleagues, friends, random internet people. Whatever the project, get to a MVP that's working well and iterate quickly. 

### You're not the only one building

A lot of people are building things with LLMs right now, there's an explosion of the number of apps people are building, but their usage is going down:

![FT app usage](/img/ft_app_usage.png)

I take a few takeaways from this:
1. Just because you built certainly doesn't mean they will come
2. Getting people to pay attention to what you build is worth spending more time & energy on

I do think there's also an explosion of low effort, low quality stuff, even as models get better. I also believe it's easier than ever to make shiny-looking demos that are appealing at first glance, yet don't hold up when used for even a few minutes. I do think having a sense of design, good product practices and iteration is more important than ever.

So:
- Iterate often
- Ship fast
- Don't let AI drive all the work
