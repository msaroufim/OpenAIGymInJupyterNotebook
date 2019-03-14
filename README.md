# How to run Open AI gym within a Jupyter notebook

I assume you're here because you wanna do ARTIFICIAL INTELLIGENCE stuff. You went to your company's ARTIFICIAL INTELLIGENCE AND MACHINE LEARNING talks and you hear people talking about "optimizing processes" and predicting house prices. You don't care about predicting house prices, you can't even afford a house or let alone rent for that matter. In fact the more you think about it, the more it triggers your anxiety.

But something in you feels incomplete, underexplored. You don't feel like you've reached your full potential. 

You tell your spouse, friends and family that you're going to get into ARTIFICIAL INTELLIGENCE. They nod at you and think that's not the worst idea. They're seen those words in the news a lot. You're feeling good, you're going to be an ARTIFICIAL INTELLIGENCE expert. You're already doing mental calculations of all the cash you'll be making and you start telling all your friends how you can't believe you didn't make this decision earlier. Then on a fateful Saturday afternoon, you sit down at your computer, you make sure you have your water bottle handy, a cup of hot coffee, some snacks. You've peed already and have told your friends and spouse not to disturb you because you're doing ARTIFICIAL INTELLIGENCE stuff.

You download Tensorflow and Open AI gym because you figure that's what you're supposed to use, you punch in a few commands in your terminal and get this.

![Let the tears flow](Capture.png)

You cry, maybe you're not smart after all. Maybe your 8th grade math teacher was right about you all along. You flake from going to your friends party because you can't address the shame of failure, especially after hyping up your ambitions so much. Maybe you're already where you're supposed to be and maybe it's better to have people that are smarter than you do ARTIFICIAL INTELLIGENCE stuff.

![I know that feel bro](wojak.jpg)

Don't worry though since there is another way  
1. Run Open AI ```gym``` on a cloud notebook provider such as [Google Collaboratory](https://colab.research.google.com) so you don't have to download anything
2. Watch your agent within the browser


## Record your agent doing stuff
We'll use a random agent

```python
import gym
from gym import wrappers

env = gym.make('SpaceInvaders-v0')
env = wrappers.Monitor(env, "./gym-results", force=True)
env.reset()
for _ in range(1000):
    action = env.action_space.sample()
    observation, reward, done, info = env.step(action)
    if done: break
env.close()
```

## Watch your agent doing stuff
The wrappers monitor library above saves a video file of the agent running a game and then

```python
import io
import base64
from IPython.display import HTML

video = io.open('./gym-results/openaigym.video.%s.video000000.mp4' % env.file_infix, 'r+b').read()
encoded = base64.b64encode(video)
HTML(data='''
    <video width="360" height="auto" alt="test" controls><source src="data:video/mp4;base64,{0}" type="video/mp4" /></video>'''
.format(encoded.decode('ascii')))
```