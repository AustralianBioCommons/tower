---
title: Create Personal Token
contributors: [Ziad Al-Bkhetan, Johan Gustafsson, Georgie Samaha]
description: 
toc: true
type: compute-environment
---


You don’t need an access token if you intend to create SSH key credentials, but you will need it for the Tower agent credentials. 

- The user can create an access token as [described here](https://help.tower.nf/latest/api/overview/?h=access+token#authentication). 
- Keep it safe, create a new one if you lose it and delete lost tokens.
- Use descriptive names.
- Don’t share your token with others.
- After you close the token creation window, you will not be able to view / copy the token again, but you can update it or delete it.

{% include callout.html type="note" content="The same personal access token can be used with multiple Tower agents, however, we recommend creating one access token for each credential or at least for each compute infrastructure." %}

