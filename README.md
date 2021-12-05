# Model-checker as a motion planner 

Consider a 2D workspace which is divided into small rectangular blocks using a grid. The size of the
workspace is 5 × 5. The lower left grid block has the ID (0, 0), and the upper right grid block has the ID (4, 4).
The blocks (2, 0), (3, 0), (1, 2), (3, 2), (1, 4), and (2, 4) are covered with obstacles. We have two robots whose
initial locations are (0, 0) and (4, 4), respectively. The robots have five motion primitives: S, L, R, U, D. The
primitive S keeps the robot in its current block in the next step. The primitives L, R, U, D take the robot from
its current block location to the left, right, upper and lower block respectively. The robots have to move to
the blocks (4, 4) and (0, 0), respectively. Moreover, The second robot should reach its destination (0, 0) strictly
after the first robot reaches its destination. Capture the behavior of the robots as a transition system and the
requirement stated above as an LTL formula. Then through model checking, synthesize a trajectory for the
robots. Use NuSMV model checker.

![Screenshot (70)](https://user-images.githubusercontent.com/87232965/144746050-e809af4e-cfa8-42fc-ae12-d75977171500.png)

## Specifications 
Robots will avoid locations with obstacles and deter to be at same location at same time,
eventually robot 1 will reach (4,4) and eventually robot 2 will reach (0,0) strictly after robot 1
will reach (4,4)(robot 1 remains at (4,4)).

## pseudo LTL 
always[~(headcollision)]  and  always[ ~((robot_coordinates =obstacles)or(collision))]
and   eventually{robot1_coordinates =(4,4) and eventually[always(robot1_coordinates =(4,4) and
eventually(robot2_coordinates =(0,0) )]}

## 
We have used !Φ in NuSMV code, because Φ is the specification that we want our model to satisfy.
!Φ will generate a counterexample and that is the trace which will satisfy Φ.

## LTL specification:
(r2x=2 & r2y=0)|(r2x=3 & r2y=0)|(r2x=3 & r2y=2) ) &F(G(r1x=4&r1y=4)&F((r1x=4&r1y=4)&(r2x=0 & r2y= 0))))
G!((Y(r2x -r1x=1& r1y=r2y)& (r1x -r2x=1& r1y=r2y))|(Y(r1x -r2x=1& r1y=r2y)& (r2x -r1x=1& r1y=r2y))|
(Y(r2y -r1y=1& r1x=r2x)& (r1y -r2y=1& r1x=r2x))|(Y(r1y -r2y=1& r1x=r2x)& (r2y -r1y=1& r1x=r2x)))&
G!((r1x=r2x& r1y=r2y)|(r1x=1& r1y=2)|(r1x=1& r1y=4)|(r1x=2& r1y=0)|(r1x=2& r1y=4)|(r1x=2& r1y=0)|
(r1x=3& r1y=0)|(r1x=3& r1y=2)|(r2x=1& r2y=2)|(r2x=1& r2y=4)|(r2x=2& r2y=0)|(r2x=2& r2y=4)|(r2x=2& r2y=0)|
(r2x=3& r2y=0)|(r2x=3& r2y=2))&F(G(r1x=4&r1y=4)&F((r1x=4&r1y=4)&(r2x=0& r2y=0)))


![Screenshot (72)](https://user-images.githubusercontent.com/87232965/144746704-4cedf590-abb7-4c5c-b7e6-72c43dba7bd7.png)

