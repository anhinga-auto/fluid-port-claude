I wanted to port Processing 2.2.1 code described in [may_9_15_experiment](may_9_15_experiment) as a project to **test the current capabilities of agentic frameworks like Claude Code**.

I started to discuss this project with both ChatGPT (GPT-5.2 Extended Thinking with Web search explicitly on) and with Claude AI (Opus 4.5 with more thinking and search on via its default).

https://chatgpt.com/share/69666681-1dd8-8010-8951-5e617f656e01

https://claude.ai/share/9376c131-2553-4fb6-9faf-51c23f10b05a

I was not quite sure what kind of system I wanted (potentially, I thought I might develop this further as a **VJing platform**, and I did not want to invest further efforts in a Processing codebase).

So the first question I asked both AI systems reflected this uncertainty:

>Hi, I am thinking about porting an interactive animation from Processing programming language to a more conventional platform (perhaps, like Python or Julia or fast JS). If I choose Python or Julia, one question is whether to use their native animation facilities, or whether to use a JS front-end (presumably connecting via websockets). I am trying to ponder the trade-offs.

In my first follow-up question, I said

>The back-end is relatively compute-heavy (it transforms images on a pixel-wise basis; although one might ponder optimization of that, but it is doing "parametric warps" of images in a rather involved fashion). For example, one of the transforms looks like this:

and then included the code for `CustomWaveTransform`. Both AI systems immediately suggested using **GPU shaders** as the best, most straightforward way.

I asked some future-looking (not immediately relevant) questions before proceeding:

>Thanks! This sounds like a convincing argument to port this to JS with shaders. If I end up needing matrix multiplication, does JS have access to a fast implementation of that?

>Thanks! On one hand, I am just pondering doing an experimental port of a piece of software, but I am also pondering possible future extensions, and I am not quite sure. One more question: recently people started to introduce autodiff in connection with some shader frameworks. In this sense, do you know of anything relevant to our current conversation?

