## Agent-Based Model
#### _Hungry like the Wolf_

The model has the purpose of creating two different types of agents: **sheep** and **wolves**. Once created, the sheep will wander through an environment that contains "food". In addition to moving, they have two more functions: _eating_ and _sharing_ units with other sheep when they come close to a certain —and predefined— distance.

The wolves, on the other hand, have the capacity of moving through the environment and _hunting_ sheep when they step into a certain distance. In addition, the sheep increase their speed the more food they eat, allowing them to escape from their predators. The model stops when all the sheep have been hunted by the wolves.

Let's take a closer look to the code. First, some parameters are defined. Here you can define the number of sheep —coded as agents— and the number of wolves yo want in the model. You can also specify the number of iterations for each agent, i.e. how many times they will _move_, _eat_, _share_ and _hunt_ (this has not been divided for each type of agent).

```python
if (isAwesome){
  return true
}
```
