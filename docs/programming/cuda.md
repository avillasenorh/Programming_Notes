# CUDA

## CUDA Python with `Numba`

`Numba` can compile for the CPU and GPU using function decorators.

For example the the `@jit` decorator acts on a function `add` by doing
`add = jit(add)`.

Not all operation/features of Python available in `Numba`. For example:

- dictionaries
- `Numpy` functions (use `math.` functions instead)

### CPU optimization in Numba

This is accomplished with the `@jit` decorator:

```python
from numba import jit
import math

@jit
def hypot(x, y):
    # Implementation from https://en.wikipedia.org/wiki/Hypot
    x = abs(x);
    y = abs(y);
    t = min(x, y);
    x = max(x, y);
    t = t / x;
    return x * math.sqrt(1+t*t)
```


