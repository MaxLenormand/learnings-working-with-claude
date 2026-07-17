Some learnings of how I've worked with Fable over the last few weeks

### Be more ambitious, less hand-holdy 
- Spend more time giving clearer instructions in the first prompt.
- Provide some inspirations whenever possible. One that's worked really well for me is passing the HTML blogpost each time I want claude to create a HTML render preview instead of a list: https://claude.com/blog/using-claude-code-the-unreasonable-effectiveness-of-html
- Give clear "done" / "not done" goals and specs: "Make a visualization that loads in less than 2s" -> Lets fable go in the background
- Providing examples. In Fused Render that's sharing with the team what's already been built so Claude has somewhere to start with (and see an example of what 'working' looks like)
- From there, I've found less need to provide super specific implementation details. A lot more of what I want rather than how I want it

### Have ways of testing fast.
- Working with small files, asking Claude to benchmark itself how fast / slow everything is so it can feel for itself it any part of the project is taking too long. This is more focused on performance for a visualization project more than anything 
- Leveraging HTML query param in Fused Render so Claude can test, see (as in headless screenshot) and benchmark the different layers, visualizations settings, toggles, etc. One example of this: 
    -> Adding `&x=40&y=70&z7=&layers=elevation` as query params any time there's a map so Claude can debug specific places / locations / zoom levels / layers that are problematic. This helps provide feedback to Claude directly + get 

### Brainstorm with Claude
- When I'm not 100% sure of what I want, I ask Claude to make 3-5 versions of the same project specifically asking it to make them differently so I cna explore ideas I hadn't even necessarily thought of before. 

### Evaluate on the output, not the code
- I basically don't read code anymore when working on these projects, at a few execptions (NOTE: This is specifically on more exploratory projects. ):
    1. Personnal curiosity -> Wanting to learn myself how LLM figured something out that I genuinely don't know myself
    2. Sanity check when intuition feels like something is off / claude is getting stuck in a loop and can't figure something out. This usually happens for:
        - Doulbe checking API key wasn't hard coded in code
        - Checking which API / files / endpoints are used when pulling data 
        -> Basiclaly every point where there's a high impact on the decision. Things that might be detials like working with elevation data, there's a big analytical difference between Digital Surface Model (shows the surface like buildings, trees, cars) and Digital *Terrain* Model which has those removed. Both are similar file sizes, formats, stats like average height & std are just slightly different but not so much so (mountains tend to be a whole lot bigger than houses) 
    3. Check for potential improvements. This is becoming less the case a smodels get better, but with Sonnet I found it often doing for loops instead of having a list comprehension in Python. Even making a skill for it didn't always solve it. This is less the case with higher models like Fable though 


### Constantly re-evaulate what I think is possible, and what my role is

Since late 2024, I've really felt like I need to *constantly* re-evaulate what I think these models can do. 
It's so easy to see posts online saying "look how dumb these models, they fail at doing the most basic X". Yes, they fail at stupid stuff. 
But so do I 
That doesn't mean there's no value in these. Especially when the target keeps moving and the stuff these models can do keeps getting better & better

### Model specific findings
- All models available with Claude (at the time of writing, July 2026) are incredibly verbose. I saw someone online (but can't find it anymore) elegantly put this: This moves the burden of work from the person building / prompting Claude to the one reading. I've noticed when I rush things, I quickly glance and don't actually read what Claude is building yet still feel the urge to ship. I actively have to fight back against Claude to tell it to make things less verbose, and contanslty remove useless, redundant or repetitive text. We should take a line out of [Blaise Pascal's book](https://www.npr.org/sections/13.7/2014/02/03/270680304/this-could-have-been-shorter) and get models to write shorter, but better. I'm still experimenting with how models can write better outputs, that are shorter and more thoughtful for projects. Either way I still write a lot for myself, to think through problems.
- Fable feels like a significant step up above Opus 4.8 (as of July 2026) in terms of the scope of what it can do. I haven't (yet) played around with other providers like Codex or Kimi. 

At the time of writing, I believe:
- AI models are getting better & better at doing more & more complex tasks 
- It's very easy to get something out of them, but there also is a ["LLM-default" look to many things](https://www.404media.co/we-are-living-in-a-chatgpt-flyer-pandemic/)
- People with domain knowledge of specific topics (I know quite a lot about satellite image processing) have a lot to gain from this tech because it's easy to describe in detail what one wants
- At the same time, having been in the same domain for many years also means one gets used to the pace of change in it. This time it does feel like I, personnaly, actively need to fight my own intuition as to what is simple and what takes a lot of effort and re-calibrate that every few months. 
