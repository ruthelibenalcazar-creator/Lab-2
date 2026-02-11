# Lab-2
public class MazeSolver {

    static int[][] maze = {
        {0,0,1,0,0,0,1,0,0,0},
        {1,0,1,0,1,0,1,0,1,0},
        {1,0,0,0,1,0,0,0,1,0},
        {1,1,1,0,1,1,1,0,1,0},
        {0,0,0,0,0,0,1,0,0,0},
        {0,1,1,1,1,0,1,1,1,0},
        {0,1,0,0,0,0,0,0,1,0},
        {0,1,0,1,1,1,1,0,1,0},
        {0,0,0,1,0,0,0,0,0,0},
        {1,1,0,1,0,1,1,1,1,0}
    };

    static boolean[][] visited = new boolean[10][10];

    public static boolean solveMaze(int row, int col) {

        // Base cases
        if (row < 0 || col < 0 || row >= maze.length || col >= maze[0].length)
            return false;

        if (maze[row][col] == 1 || visited[row][col])
            return false;

        if (row == maze.length - 1 && col == maze[0].length - 1)
            return true;

        visited[row][col] = true;

        // Recursive case
        return solveMaze(row + 1, col) ||
               solveMaze(row - 1, col) ||
               solveMaze(row, col + 1) ||
               solveMaze(row, col - 1);
    }

    public static void main(String[] args) {
        if (solveMaze(0, 0))
            System.out.println("Path found!");
        else
            System.out.println("No path exists.");
    }
}