---
layout: ../../layouts/BlogPostLayout.astro
date: "2025-05-26"
title: "The Beauty of Colocating"
description: "Keep relevant things close together. It will save you time later."
status: "published"
---

### Context

I recently ventured to my grandparents' house for a weekend stay. Oftentimes, they prepare a list of technology-related-things that I can help them with while I'm there. Being the "techie" in the family often gets you into this debacle! Though, it's a pretty good deal considering that I'm **very** well fed in exchange.

On this occasion, one of the things that my grandpa needed help with was re-connecting his hearing aids to their living room television. This way, my grandma wouldn't yell at him for having the volume too loud to compensate for the fact the audio was no longer playing directly in his ear. I fixed it up pretty quickly by clicking the pair button at the back of the Unitron TV Connector if anyone else ever has to solve this...

While my grandpa's pretty neat, his memory isn't the greatest, so he keeps his instruction booklets in a place that will be intuitive to find if he ever runs into an issue. In this case, after I had finished fixing the issue for him, he put the instructions for the TV Connector back in the entertainment centre below the television.

### Lightbulb

This sparked a thought - we do this all the time as software engineers; keeping things close to where they need to be. For example, we might add the occasional in-line code comment to explain a decision, error code, or a weird one-liner in a function, or even just to add a link to some documentation or a ticket. Oftentimes, it's because we might forget why we did it later, or we think that future maintainers and/or our current team may benefit from it.

The word for this is **colocate**. It means to place two or more things close together due to relevance or the need to share common facilities.

### Applications

At my work, I see opportunities to adhere to this principle all the time. For example, I much prefer adding comments to my code directly over documenting elsewhere, for 2 reasons:

1. In general, humans will choose the easy option.
   - If somone needs to understand your code in future, they likely won't be bothered to spend hours searching `INSERT-SAAS-DOCUMENTATION-PLATFORM-HERE` for why a specific decision was made (if you didn't link it). By keeping the justification for decisions close to what they are interacting with, it decreases effort-to-understand.
2. Documentation will always get out of date eventually - see [Thorbjørn Sigberg's Laws of Documentation](https://medium.com/@thorbjorn.sigberg/sigbergs-laws-of-documentation-fab155b2415b).
   - If you keep your documentation in a different place to your code, you significantly reduce the chance that someone will be bothered to adjust it. Make it easy for them (see dot point 1) by having it close to where they are making the change.

### Wrapping Up

As working professionals (not just software engineers), I think we would do well to colocate things better. Don't spend thousands of dollars on documentation platforms if you can add documentation close to where it needs to be instead.

I highly recommend watching [The Unreasonable Effectiveness Of Plain Text by No Boilerplate](https://www.youtube.com/watch?v=WgV6M1LyfNY) if you want to learn more about how you can do this.
