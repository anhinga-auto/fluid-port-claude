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

At this point, I paused the conversation with ChatGPT and continued only with Claude AI (in part, because it was more crisp with the last question, and I did not want to get too involved in that cul-de-sac, in part, because I wanted to start with Claude Code for a number of reasons (everyone was talking about it, so more was known about it; also ChatGPT had always been my main AI platform, and I knew that agentic use affects the situation (e.g. with usage limits, and other factors, for example, ChatGPT used to ask to turn 2FA on if one was trying to use Codex (which was the reason, I turned it on back when I first looked at Codex a while ago ;-)), so I thought it was better to experiment first in a platform which was less essential for me day-to-day so far)).

Claude Opus 4.5:

>... Would you like me to search for the current state of any of these—particularly Taichi's web story or Slang's toolchain?

ME:

>Thanks! Yes, I'd love to be more up to date in this sense.

>Thanks! Rose is very interesting, I have not known about it. Unfortunately, it progressed to 0.4.10 in April 2024 and then stopped progressing. Yes, I think it makes sense to start with plain shaders for now. I am going to prepare a project for Claude Code. How should I instruct Claude Code? (I'll create a dedicated GitHub repository for this project, and I'll have a subdirectory with Processing code to be ported. I'd like an equivalent JS-oriented shader-based version and the instructions for how to run it. Where should I put the information for Claude Code in that repository?)

At that Claude AI gave me a suggested structure of the project and a sketch for CLAUDE.md (and I lightly edited all that, in particular, choosing WebGL2 over WebGPU and keeping my old name for the directory containing Processing code).

Then I asked 

>Thanks! You have this nice shader prototype above for the warp. Should I place it somewhere as an example, or should I just let Claude Code to cook?

and Claude Opus 4.5 suggested that it might be a good idea to put that right into CLAUDE.md, but when I started working with Claude Code I forgot to do that, and it was fine, there was no need to do that (I was using Sonnet 4.5 under Claude Code, because that was all that's available at a minimal paid plan (with the minimal payment plan, Opus 4.5 was available only in Chat, but not in Claude Code) and Opus 4.5 was a smarter system, but Sonnet 4.5 was pretty smart too and often sufficient).

***

At this point I started to set-up Claude Code (on the web). Earlier, I had dialogs with both Claude AI and ChatGPT about using Claude Code on the web and Codex on the web respectively:

https://claude.ai/share/c7fa8e9b-64bb-47a9-8756-c3ebd75ba45e

https://chatgpt.com/share/696493f7-949c-8010-843b-397f57cbce6a

ChatGPT was much more fluent speaking about Codex, whereas Claude AI had to be convinced that Claude Code on the web exists, but afterwards it gave good information.

ME, successfully convincing Opus 4.5:

>This seems to say I can run it on the cloud: https://claude.ai/code/onboarding

One of the reasons for this difference was that running on the web in a host company sandbox was the main original form of Codex, whereas for Claude Code this option had been added recently. 

Then Opus 4.5 got confused again and started to give me references to Cursor, I had to convince it again to look at the system I wanted to use:

ME:

>No, I don't think this has anything to do with Cursor IDE. I am not using Cursor. I'll be using this: https://claude.ai/code/onboarding

Opus 4.5:

>Let me check the official Claude Code documentation for the specific web onboarding process.
>
>Now I have the official documentation. Here's how connecting GitHub works for Claude Code on the web:
>
>**The setup process:**
>
> 1. Visit claude.ai/code
> 2. Connect your GitHub account
> 3. Install the Claude GitHub app in your repositories
> 4. Select your default environment
> 5. Submit your coding task

>**It uses a GitHub App, not fine-grained tokens:**
>
>Claude Code on the web uses a **GitHub App** that you install on your repositories, rather than fine-grained personal access tokens that you'd create yourself. When you install the app, you choose which repositories to grant access to.
>
>**How the security works behind the scenes:**
>
>All GitHub operations go through a dedicated proxy service. Inside the sandbox, the git client authenticates using a custom-built scoped credential. The proxy:
>
> * Manages GitHub authentication securely—the git client uses a scoped credential inside the sandbox, which the proxy verifies and translates to your actual GitHub authentication token
> * Restricts git push operations to the current working branch for safety
> * Enables cloning, fetching, and PR operations while maintaining security boundaries
>
>Your actual GitHub credentials are never inside the sandbox with Claude Code. Authentication is handled through the secure proxy using scoped credentials.
>
>**So in short:** You don't need to manually create tokens. You install the Claude GitHub App, select which repositories it can access, and the system handles authentication securely through a proxy that limits what Claude can do (like only pushing to the current working branch).



