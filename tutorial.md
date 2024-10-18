# ASE NEB Calculation Example

The following example demonstrates how to perform NEB calculations using ASE with the AIMS calculator.

```python
from ase import io
from ase.mep.neb import NEB
from ase.optimize import BFGS
from ase.calculators.aims import Aims
from ase.optimize import MDMin
from ase.constraints import FixAtoms
from ase.io import Trajectory

# Define a function to create a new calculator instance
def create_calc():
    return Aims(xc='pbe', spin='none', k_grid=(2, 2, 1), relativistic=('atomic_zora', 'scalar'),
                compute_forces='.true.', tier=1)

# Read initial and final states
initial = io.read(filename='initial.in', format='aims')
final = io.read(filename='final.in', format='aims')

# Constraint instance
mask = [i == 0 for i in range(250)]  # now first atom is our migrating atom
constraint = FixAtoms(mask=mask)
# initial.set_constraint(constraint)
# final.set_constraint(constraint)
