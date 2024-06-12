import turtle



pen=turtle.Turtle()

font_size = 20
font_color = "red"
font_style = ("Arial", font_size, "bold")

# Write the message
message = "PING PONG\n"
pen.penup()
pen.goto(0, 0)
pen.color(font_color)
pen.write(message, align="center", font=font_style)
message = "     here the score is increased \nwhen you miss a ball"
pen.penup()
pen.goto(-50, -50)
pen.color(font_color)
pen.write(message, align="center", font=font_style)
message = "Player 1: white\nPlayer 2: cyan\n"
pen.penup()
pen.goto(-250, -250)
pen.color(font_color)
pen.write(message, align="center", font=font_style)
message = "player 1: up and down arrow\n player 2: w and s key"
pen.penup()
pen.goto(200, -250)
pen.color(font_color)
pen.write(message, align="center", font=font_style)
# Set up the screen

screen = turtle.Screen()
screen.title("Ping Pong")
screen.bgcolor("black")
screen.setup(width=800, height=600)
screen.tracer(0)

# Create the paddle A
paddle_a = turtle.Turtle()
paddle_a.speed(0)
paddle_a.shape("square")
paddle_a.color("cyan")
paddle_a.shapesize(stretch_wid=6, stretch_len=1)
paddle_a.penup()
paddle_a.goto(-350, 0)

# Create the paddle B
paddle_b = turtle.Turtle()
paddle_b.speed(0)
paddle_b.shape("square")
paddle_b.color("white")
paddle_b.shapesize(stretch_wid=6, stretch_len=1)
paddle_b.penup()
paddle_b.goto(350, 0)

# Create the ball
ball = turtle.Turtle()
ball.speed(40)
ball.shape("circle")
ball.color("white")
ball.penup()
ball.goto(0, 0)
ball.dx = 0.3
ball.dy = -0.3
# Create score variables
score_a = 0
score_b = 0

# Create the score display
score_display = turtle.Turtle()
score_display.speed(0)
score_display.color("white")
score_display.penup()
score_display.hideturtle()
score_display.goto(0, 260)
score_display.write("Player A: {}  Player B: {}".format(score_a, score_b), align="center", font=("Arial", 24, "normal"))



# Functions to move the paddles
def paddle_a_up():
    y = paddle_a.ycor()
    if y < 250:
        y += 20
    paddle_a.sety(y)

def paddle_a_down():
    y = paddle_a.ycor()
    if y > -250:
        y -= 20
    paddle_a.sety(y)

def paddle_b_up():
    y = paddle_b.ycor()
    if y < 250:
        y += 20
    paddle_b.sety(y)

def paddle_b_down():
    y = paddle_b.ycor()
    if y > -240:
        y -= 20
    paddle_b.sety(y)

# Keyboard bindings
screen.listen()
screen.onkeypress(paddle_a_up, "w")
screen.onkeypress(paddle_a_down, "s")
screen.onkeypress(paddle_b_up, "Up")
screen.onkeypress(paddle_b_down, "Down")

# Main game loop
while True:
    screen.update()

    # Move the ball
    ball.setx(ball.xcor() + ball.dx)
    ball.sety(ball.ycor() + ball.dy)

    # Check collision with the top and bottom walls
    if ball.ycor() > 290:
        ball.sety(290)
        ball.dy *= -1

    elif ball.ycor() < -290:
        ball.sety(-290)
        ball.dy *= -1

    # Check collision with the paddles
    if (ball.dx > 0) and (350 > ball.xcor() > 340) and (paddle_b.ycor() + 50 > ball.ycor() > paddle_b.ycor() - 50):
        ball.color("blue")
        ball.setx(340)
        ball.dx *= -1

    elif (ball.dx < 0) and (-350 < ball.xcor() < -340) and (paddle_a.ycor() + 50 > ball.ycor() > paddle_a.ycor() - 50):
        ball.color("green")
        ball.setx(-340)
        ball.dx *= -1

     #Check if ball is out of bounds
    if ball.xcor() > 390:
        ball.goto(0, 0)
        ball.dx *= -1
        score_a += 1
        score_display.clear()
        score_display.write("Player A: {}  Player B: {}".format(score_a, score_b), align="center", font=("Arial", 24, "normal"))


    elif ball.xcor() < -390:
        ball.goto(0, 0)
        ball.dx *= -1
        score_b += 1
        score_display.clear()
        score_display.write("Player A: {}  Player B: {}".format(score_a, score_b), align="center", font=("Arial", 24, "normal"))
        
    
turtle.done()

