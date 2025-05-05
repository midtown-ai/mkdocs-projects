title: Intermediate Python > Object
---

--8<-- [start:body]
## Object

```python
class Vector2D:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        if isinstance(other, Vector2D):
            return Vector2D(self.x + other.x, self.y + other.y)
        return NotImplemented

    def __mul__(self, scalar):
        if isinstance(scalar, (int, float)):
            return Vector2D(self.x * scalar, self.y * scalar)
        return NotImplemented

    def __rmul__(self, scalar):
        return self.__mul__(scalar)  # for scalar * vector

    def __repr__(self):
        return f"Vector2D({self.x}, {self.y})"
```
--8<-- [end:body]
