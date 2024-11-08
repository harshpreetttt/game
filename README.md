import tkinter as tk
import random

class CatchTheBallGame:
    def __init__(self, root):  # Corrected constructor
        self.root = root
        self.root.title("Catch the Ball")
        self.root.geometry("500x500")
        self.root.configure(bg="lightblue")
        self.score = 0
        self.ball_size = 30
        
        # Score label
        self.score_label = tk.Label(root, text=f"Score: {self.score}", font=("Arial", 16), bg="lightblue")
        self.score_label.pack(pady=10)
        
        # Canvas for the game
        self.canvas = tk.Canvas(root, width=500, height=400, bg="white")
        self.canvas.pack()
        
        # Create the ball
        self.ball = self.canvas.create_oval(10, 10, self.ball_size, self.ball_size, fill=self.random_color())
        self.canvas.tag_bind(self.ball, "<Button-1>", self.catch_ball)
        
        # Start moving the ball
        self.move_ball()

    def move_ball(self):
        x = random.randint(0, 500 - self.ball_size)
        y = random.randint(0, 400 - self.ball_size)
        self.canvas.coords(self.ball, x, y, x + self.ball_size, y + self.ball_size)
        self.canvas.itemconfig(self.ball, fill=self.random_color())
         self.roota.after(2000, self.move_ball)  # Move the ball every 2 seconds

    def catch_ball(self, event):
        self.score += 1
        self.score_label.config(text=f"Score: {self.score}")
        self.move_ball()  # Move the ball immediately after it's clicked

    def random_color(self):
        # Generate a random color
        return f"#{random.randint(0, 255):02x}{random.randint(0, 255):02x}{random.randint(0, 255):02x}"

# Corrected if condition for running the main program
if __name__ == "__main__":
    root = tk.Tk()
    game = CatchTheBallGame(root)
    root.mainloop()
