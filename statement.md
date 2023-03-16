import random
import turtle

# create window
win = turtle.Screen()
win.title("Pong")
win.bgcolor("black")
win.setup(width=600, height=400)

# create paddles
paddle_a = turtle.Turtle()
paddle_a.speed(0)
paddle_a.shape("square")
paddle_a.color("white")
paddle_a.shapesize(stretch_wid=5, stretch_len=1)
paddle_a.penup()
paddle_a.goto(-250, 0)

paddle_b = turtle.Turtle()
paddle_b.speed(0)
paddle_b.shape("square")
paddle_b.color("white")
paddle_b.shapesize(stretch_wid=5, stretch_len=1)
paddle_b.penup()
paddle_b.goto(250, 0)

# create ball
ball = turtle.Turtle()
ball.speed(0)
ball.shape("circle")
ball.color("white")
ball.penup()
ball.goto(0, 0)
ball.dx = 3
ball.dy = -3

# create scoreboard
score_a = 0
score_b = 0
scoreboard = turtle.Turtle()
scoreboard.speed(0)
scoreboard.color("white")
scoreboard.penup()
scoreboard.hideturtle()
scoreboard.goto(0, 170)
scoreboard.write("Player A: {}  Player B: {}".format(score_a, score_b), align="center", font=("Courier", 16, "normal"))

# define paddle movement functions
def paddle_a_up():
    y = paddle_a.ycor()
    y += 20
    paddle_a.sety(y)

def paddle_a_down():
    y = paddle_a.ycor()
    y -= 20
    paddle_a.sety(y)

def paddle_b_up():
    y = paddle_b.ycor()
    y += 20
    paddle_b.sety(y)

def paddle_b_down():
    y = paddle_b.ycor()
    y -= 20
    paddle_b.sety(y)

# set up keyboard bindings
win.listen()
win.onkeypress(paddle_a_up, "w")
win.onkeypress(paddle_a_down, "s")
win.onkeypress(paddle_b_up, "Up")
win.onkeypress(paddle_b_down, "Down")

# game loop
while True:
    win.update()

    # move ball
    ball.setx(ball.xcor() + ball.dx)
    ball.sety(ball.ycor() + ball.dy)

    # check for collision with walls
    if ball.ycor() > 190 or ball.ycor() < -190:
        ball.dy *= -1

    # check for collision with paddles
    if ball.xcor() > 240 and ball.xcor() < 250 and (ball.ycor() < paddle_b.ycor() + 50 and ball.ycor() > paddle_b.ycor() - 50):
        ball.dx *= -1
        score_b += 1
        scoreboard.clear()
        scoreboard.write("Player A: {}  Player B: {}".format(score_a, score_b), align="center", font=("Courier", 16, "normal"))

    if ball.xcor() < -240 and ball.xcor() > -250 and (ball.ycor() < paddle_a.ycor() + 50 and ball.ycor() > paddle_a.ycor() - 50):
        ball.dx *= -1
        score_a += 1
        scoreboard.clear()
        scoreboard.write("Player A: {}  Player B: {}".format(score_a, score_b), align="center", font=("Courier", 16, "normal
