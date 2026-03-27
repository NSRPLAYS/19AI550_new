# Ex.No: 10  Implementation of 3D snake game 
### DATE: 27/03/26                                                                          
### REGISTER NUMBER : 212224240103 
### AIM: 
To develop a 3D snake game in Unity 
### Algorithm:
1. Create a New Unity Project by opening Unity Hub and creating a new 3D project. Name the project SnakeGame.
2. Create a play area in the scene using a plane or cube for the ground, and add boundary walls around it so the snake has a visible movement space.
3. Create a SnakeHead GameObject and a SnakeBodySegment prefab, then write a SnakeController.cs script to control movement, direction, and growth.
4. Create a Food GameObject and write a FoodSpawner.cs script to spawn food at random valid positions inside the play area.
5. Create an empty GameObject named GameManager and attach a GameManager.cs script to manage score, game state, restart, and game-over logic.
6. Write the Snake movement algorithm so that on each tick the head moves forward, body segments follow, food increases length and score, and collisions with walls or self end the game.
7. Create a simple UI Canvas with score text and a game-over/restart prompt, then connect keyboard input like W/A/S/D or arrow keys to control the snake.

### Program:
```
using System.Collections.Generic;
using UnityEngine;

public class SnakeLogic : MonoBehaviour
{
    public int width = 20, height = 20;
    List<Vector2Int> snake = new() { new(5, 5), new(4, 5), new(3, 5) };
    Vector2Int direction = Vector2Int.right;
    Vector2Int food = new(8, 5);
    int score = 0;
    bool gameOver = false;

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.W)) direction = Vector2Int.up;
        if (Input.GetKeyDown(KeyCode.S)) direction = Vector2Int.down;
        if (Input.GetKeyDown(KeyCode.A)) direction = Vector2Int.left;
        if (Input.GetKeyDown(KeyCode.D)) direction = Vector2Int.right;
    }

    public void MoveSnake()
    {
        if (gameOver) return;

        Vector2Int head = snake[0] + direction;

        if (head.x < 0 || head.x >= width || head.y < 0 || head.y >= height || snake.Contains(head))
        {
            gameOver = true;
            return;
        }

        snake.Insert(0, head);

        if (head == food)
        {
            score++;
            food = NewFood();
        }
        else
        {
            snake.RemoveAt(snake.Count - 1);
        }
    }

    Vector2Int NewFood()
    {
        Vector2Int p;
        do
        {
            p = new Vector2Int(Random.Range(0, width), Random.Range(0, height));
        } while (snake.Contains(p));
        return p;
    }
}

```
### Output:
<img width="1909" height="1199" alt="image" src="https://github.com/user-attachments/assets/7a1d6b35-ccc4-4737-8ad9-6a16a4c3ecb8" />

### Result:
Thus the 3D snake game was developed using Unity
