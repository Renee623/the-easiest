# the-easiest
day1
using static System.Console;
namespace ConsoleApp24 {
    class Program {

        static void Main(string[] args) {
            Random rand = new Random();
            int foodx = rand.Next(0,20);
            int foody = rand.Next(0,20);
            int score = 0;
            int row = 0;
            int col = 0;
            List<(int x, int y)> snake = new List<(int x, int y)>();
            snake.Add((4, 4));
            while (true)
            {
                Clear();
                WriteLine($"分数:{score}");
                WriteLine("+————————————————————+");
                for (row = 0; row < 20; row++)
                {
                    Write("|");
                    for (col = 0; col < 20; col++)
                    {


                        
                        bool isSnake = false;
                        foreach (var segment in snake)
                        {

                            if (col == segment.x && row == segment.y)
                            {
                                isSnake = true;
                                break;

                            }
                        }
                        if (isSnake)
                        {

                            if (col == snake[0].x && row == snake[0].y)
                            {

                                Write("O");
                            }
                            else
                            {
                                Write("x");
                            }

                        }
                        else if (col == foodx && row == foody) {

                            Write("$");
                        }
                        else
                        {
                            Write(" ");

                        }


                    }
                    WriteLine("|");
                }
                WriteLine("+————————————————————+");

                int headx = snake[0].x;
                int heady = snake[0].y;

                int newheadx = headx;
                int newheady = heady;
                ConsoleKeyInfo key = ReadKey(true);
                switch (key.Key) {

                    case ConsoleKey.W:newheady--;break;
                    case ConsoleKey.S:newheady++;break;
                    case ConsoleKey.A:newheadx--;break;
                    case ConsoleKey.D:newheadx++;break;
                
                }
                if (newheadx < 0 || newheadx >= 20 || newheady < 0 || newheady >= 20) {

                    Clear();
                    WriteLine("触礁了");
                    ReadKey();
                    return;
                }
                bool hitself = false;
                foreach (var segment in snake) {

                    if (segment.x == newheadx && segment.y == newheady) {
                        hitself = true;
                        break;
                    }
                
                }
                if (hitself) {
                    Clear();
                    WriteLine("太不小心了，怎么撞到自己了呀");
                    ReadKey();
                    return;
                }
                snake.Insert(0, (newheadx, newheady));
                if (newheadx == foodx && newheady == foody)
                {
                    score++;
                    bool onSnake;
                    do
                    {
                        foodx = rand.Next(0, 20);
                        foody = rand.Next(0, 20);
                        onSnake = false;
                        foreach (var segment in snake)
                        {

                            if (segment.x == foodx && segment.y == foody)
                            {

                                onSnake = true;
                                break;
                            }
                        }

                    } while (onSnake);
                }
                else {
                    snake.RemoveAt(snake.Count - 1);
                
                }
            }
        
        
        }
    
    
    
    
    
    }










}
