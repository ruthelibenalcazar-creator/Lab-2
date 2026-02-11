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

    static boolean[][] visited;

    /**
     * Recursively attempts to find a path from (row, col)
     * to the exit (n-1, n-1) using DFS.
     */
    public static boolean solveMaze(int row, int col) {
        int n = maze.length;

        // Base case 1: Out of bounds
        if (row < 0 || col < 0 || row >= n || col >= n)
            return false;

        // Base case 2: Wall or already visited
        if (maze[row][col] == 1 || visited[row][col])
            return false;

        // Base case 3: Exit reached
        if (row == n - 1 && col == n - 1) {
            maze[row][col] = 2; // Mark exit as part of path
            return true;
        }

        // Mark current cell as visited
        visited[row][col] = true;

        // Recursive case: Explore 4 directions
        if (solveMaze(row + 1, col) ||   // Down
            solveMaze(row - 1, col) ||   // Up
            solveMaze(row, col + 1) ||   // Right
            solveMaze(row, col - 1)) {   // Left

            maze[row][col] = 2; // Mark path
            return true;
        }

        return false;
    }

    // Utility method to print maze
    public static void printMaze() {
        for (int[] row : maze) {
            System.out.println(Arrays.toString(row));
        }
    }

    public static void runTest(String testName, int startRow, int startCol) {
        visited = new boolean[maze.length][maze[0].length];

        System.out.println("\n=== " + testName + " ===");
        boolean result = solveMaze(startRow, startCol);
        System.out.println("Path found? " + result);
        printMaze();
    }

    public static void main(String[] args) {

        // Test 1: Normal case
        runTest("Test 1: Start at (0,0)", 0, 0);

        // Test 2: Start is a wall
        int original = maze[0][0];
        maze[0][0] = 1;
        runTest("Test 2: Start is a wall", 0, 0);
        maze[0][0] = original;

        // Test 3: Out of bounds
        runTest("Test 3: Start out of bounds", -1, 0);
    }
}