[⬅️ previous](exercise2.md) | [inbox](readme.md) 

# ML Ops 3: Scheduling Overhead

Good 

Thank you for the solution to our timeout problems!. It has been a week, and the rovers are no 
longer deadlocking on long computation times.

Folks from the sustainability lab were able to get a lot of useful data about the
model behavior. They could improve it even further.

This improvement comes at a cost - **it takes the model some time to initialize**. Fortunately, once the model is ready, 
it could be reused for multiple computations. 

Attached you will find [model3.py](model3.py) which simulates this kind of behavior.

Once started, the model will start initializing immediately. Once done and ready to accept requests
it print `ready: Model-initialized` to the `stdout`.

From this point you can send multiple requests to the model via `stdin`. Each request must be a valid JSON on a single line 
that ends with a newline `\n`. If there is no incoming data on the `stdin` the model will
just wait for it to arrive (as long as `stdin` stays open).

Here is an example that launches the model and sends two requests two it:

```
director@mex25pl ice-seeker (overhead)> echo "{\"data\":2}\n{\"data\":3}\n" | python model3.py
initializing model...
 0
 1
 2
 3
 4
ready: Model-initialized
Loading data from the stdin
input: {"data": 2}
Start calculations
Done in 2.19sec
result: {"ice_found": true}
input: {"data": 3}
Start calculations
Done in 0.14sec
result: {"ice_found": true}
```

Our hardware supports running 4 models in parallel. We want to use this capacity 100% and maximize the throughput.

Could you, please, figure out how to support this new model efficiently? Ideally, we want to have it before the winter solstice MY39.

Counting on you,  
Colony Director

<img src="https://www.nasa.gov/sites/default/files/styles/ubernode_alt_horiz/public/thumbnails/image/emc-poster-astro-hab-lores.jpg">

# Task

Please adjust your API to preload 4 models on start-up. When a request comes in, the first
available model would pick it up, compute and return the response right away. 

Please keep in mind: if a model is killed with a timeout (or just raises an exception) then it must be replaced by a new model.

Please feel free to send PRs that add your solution to this list.

- [Your Name](http://github.com/your-github-profile): [programming language](http://github.com/url-to-the-ml-ops-solution-3)



