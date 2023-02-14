# Distance heuristics

Using approximation heuristics is generally less time consuming than exact heuristic methods.

There are generally three approximation heuristics to calculate a distance between 2 points on a 2D grid.

![](https://images.unsplash.com/photo-1463681457836-cc9f3f99608b?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1470&q=80)

📷 by [Pablo García Saldaña](https://unsplash.com/@garciasaldana_)

## Manhattan distance
When we are allowed to move only in four directions only (right, left, top, bottom) :

    h = abs(current_cell.x – goal.x) + 
        abs(current_cell.y – goal.y)

## Diagonal distance
When we are allowed to move in eight directions only (similar to a move of a King in Chess) :

    dx = abs(current_cell.x – goal.x)
    dy = abs(current_cell.y – goal.y)
    
    h = D * (dx + dy) + (D2 - 2 * D) * min(dx, dy)

    where D is length of each node (usually = 1) and D2 is diagonal distance between each node (usually = sqrt(2) ).

## Euclidean distance
When we are allowed to move in any directions :

    h = sqrt(
            (current_cell.x – goal.x)**2 + 
            (current_cell.y – goal.y)**2
        )
