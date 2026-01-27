# What Are Namespaces?

A namespace is a container that holds a group of identifiers ([[variables]], [[functions]], [[classes]], etc.) and keeps them separate from identifiers in other namespaces. 

>It's a way to organize code and prevent **naming conflicts** by grouping related code together under a unique name.

## Analogy

Think of namespaces like different departments:

- **Marketing Department**: employee "John Smith"
- **Engineering Department**: Also employee "John Smith"
- **HR Department**: Also employee "John Smith"

To identify which John Smith you're talking about, you specify the department:  e.g. "Marketing's John Smith"

>The department name acts as a namespace that prevents confusion.

---

**In Programming:**

- `Math.max()` — the `max` function *in* the `Math` namespace
- `String.max()` — the `max` function *in* the `String` namespace 

# Pratical Example

``` Java
// Package acts as namespace
package com.mycompany.utilities;

public class Calculator {
    public static int add(int a, int b) {
        return a + b;
    }
}

// In another file
package com.othercompany.utilities;

public class Calculator {  // Same class name, different package/namespace
    public static double add(double a, double b) {
        return a + b;
    }
}

// Using them
import com.mycompany.utilities.Calculator as MyCalc;
import com.othercompany.utilities.Calculator as OtherCalc;

MyCalc.add(5, 3);      // Uses first Calculator
OtherCalc.add(5.0, 3.0);  // Uses second Calculator
```


# Common Namespace Concepts

## Nested Namespaces

You can have namespaces within namespaces (like folders within folders):

``` cpp
namespace Company {
    namespace Engineering {
        namespace Backend {
            void deploy() { }
        }
    }
}

// Access: Company::Engineering::Backend::deploy()
```

## Using/Importing Namespaces

You can bring a namespace into your current [[Scope]]:

``` python
from math import sqrt, pow  # Import specific functions
# or
from math import *          # Import everything (not recommended)

# Now you can use sqrt() directly instead of math.sqrt()
```

## Global Namespace

The default namespace where things exist if not explicitly placed elsewhere.

## Namespace vs Scope

- **[[Scope]]**: Determines _where_ a variable can be accessed (visibility and lifetime)
- **Namespace**: Determines what name identifies a variable (organizational grouping)

>[!NOTE]
>A variable can be in the global scope but still belong to a specific namespace.


#programming #namespaces #organization #modules #scope #code-structure #fundamentals