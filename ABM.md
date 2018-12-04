## Agent-Based Model
#### _Hungry like the Wolf_

The model has the purpose of creating two different types of agents: **sheep** and **wolves**. Once created, sheep will wander through an environment containing resources or "food". In addition, they have two more functions: _eating_ and _sharing_ units with other sheep when they come close to a certain —and predefined— distance.

The wolves, on the other hand, have the capacity of moving through the environment and _hunting_ sheep when they step into a certain distance from them. The sheep's _moving_ function allows them to increase their speed the more food they eat, allowing them to escape from their predators. The model stops when all the sheep have been hunted by the wolves.

Let's take a closer look into the code. First, some parameters are defined. Here you can define the number of sheep —coded as _agents_— and wolves you want in the model. You can also specify the number of iterations for each agent, i.e. how many times they will _move_, _eat_, _share_ and _hunt_ (this has not been divided for each type of agent). Finally, the _neighourhood_ parameter specifies the distance a sheep needs to be from another in order to share resources, whilst the _scope_ parameter defines the hunting distance for each wolf.
```python
num_of_agents = 15
num_of_wolves = 50
num_of_iterations = 10
neighbourhood = 20
scope = 10
```
As mentioned before, sheep will move around the environment and their speed will depend on how much food they have stored. In this example, they move **1 unit plus the 0.5% of what they have eaten so far**. We don't want them to be extremely fast! However, this could be changed if needed.
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
_Eating_ and _sharing_ resources are important behaviours for our sheep. This will allow them to store food —and thus be harder to hunt— as well as colaborate with other colleagues by equally dividing the sum of both of their food. Sheep will eat 10 units of food provided that there are more than 10 units of food in the position where they are "standing"; otherwise they eat will whatever is left in their current position.
```python
def eat(self): 
        if self.environment[self.y][self.x] > 10:
            self.environment[self.y][self.x] -= 10
            self.store += 10
        else: 
            self.environment[self.y][self.x] < 10
            self.store += self.environment[self.y][self.x]
            self.environment[self.y][self.x] -= self.environment[self.y][self.x]
            
    def share_with_neighbours(self, neighbourhood):
        for i in self.agents_list:
            if i != self: 
                distance = self.distance_between(i) 
                if distance <= neighbourhood: 
                    ave = (self.store + i.store)/2 
                    self.store = ave
                    i.store = ave
```
Wolves share the _move_ function with the sheep with the difference that their behaviour does not depend on food; instead they can only move 2 units per iteration. They also have a unique function called _hunt_ with which they are able to delete agents from the environment if they are within their _scope_.
```python
def hunt(self, agents_list):
        for i in agents_list:
            distance = self.distance_between(i) 
            if distance <= self.scope:
               agents_list.remove(i)
```
Below you can see a snapshot of the model. Wolves are represented by dark circles and sheep by yellow stars.
![Model Snapshot](/images/model_photo.jpg)

The model can be accessed through my repository by clicking [here](https://github.com/Ant-Ross/Programming-for-Social-Sciences/tree/master/Python_exercise/Final_model). Just note the quantitity of sheep and wolves you use, if there are way more sheep than wolves the model can take a while stop and in that case you might want to get yourself a cuppa and enjoy the model.

