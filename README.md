
def solve_maze(maze, x, y, path, visited):
    if x < 0 or y < 0 or x >= len(maze) or y >= len(maze[0]) or maze[x][y] == 1 or visited[x][y]:
        return False
    if x == len(maze)-1 and y == len(maze[0])-1:
        path.append((x, y))
        return True
    visited[x][y] = True
    path.append((x, y))
    if (solve_maze(maze, x+1, y, path, visited) or 
        solve_maze(maze, x, y+1, path, visited) or 
        solve_maze(maze, x-1, y, path, visited) or 
        solve_maze(maze, x, y-1, path, visited)):
        return True
    path.pop()
    return False

def print_maze(maze, path):
    for i in range(len(maze)):
        for j in range(len(maze[0])):
            if (i, j) in path:
                print('*', end=' ')
            elif maze[i][j] == 1:
                print('            
            else:
                print('#', end=' ')
            else:
                print('.', end=' ')
        print()

maze = [
    [0, 0, 1, 0, 0],
    [0, 0, 1, 0, 0],
    [0, 0, 0, 0, 1],
    [0, 1, 1, 0, 0],
    [0, 0, 0, 0, 0]
]

visited = [[False for _ in range(len(maze[0]))] for _ in range(len(maze))]
path = []

if solve_maze(maze, 0, 0, path, visited):
    print("Path found:")
    print_maze(maze, path)
else:
    print("No path found")
