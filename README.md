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
