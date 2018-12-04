## Agent-Based Model
#### _Hungry like the Wolf_

The model has the purpose of creating two different types of agents: **sheep** and **wolves**. Once created, the sheep will wander through an environment that contains "food". In addition to moving, they have two more functions: _eating_ and _sharing_ units with other sheep when they come close to a certain —and predefined— distance.

The wolves, on the other hand, have the capacity of moving through the environment and _hunting_ sheep when they step into a certain distance. In addition, the sheep increase their speed the more food they eat, allowing them to escape from their predators. The model stops when all the sheep have been hunted by the wolves.

Let's take a closer look to the code. First, some parameters are defined. Here you can define the number of sheep —coded as agents— and the number of wolves you want in the model. You can also specify the number of iterations for each agent, i.e. how many times they will _move_, _eat_, _share_ and _hunt_ (this has not been divided for each type of agent). Finally, the _neighourhood_ parameter specifies the distance a sheep needs to be from another in order to share resources and the _scope_ parameter defines the hunting distance for each wolf.

```python
num_of_agents = 15
num_of_wolves = 50
num_of_iterations = 10
neighbourhood = 20
scope = 10
```
As mentioned before, sheep will move around the environment and their speed will depend on how much food they have stored. In this example, they move **1 unit plus the 0.5%** of what they have eaten so far. We don't want them to be extremely fast! although this could be changed if needed.

```python
 def move(self):
        if random.random() < 0.5:
            self.y = (self.y + 1 + int(0.005 * self.store)) % 300 
        else:
            self.y = (self.y - 1 - int(0.005 * self.store)) % 300
            
        if random.random() < 0.5:
            self.x = (self.x + 1 + int(0.005 * self.store)) % 300
        else:
            self.x = (self.x - 1 - int(0.005 * self.store)) % 300
```
            
