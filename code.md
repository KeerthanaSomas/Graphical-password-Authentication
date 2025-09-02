import tkinter as tk
from tkinter import messagebox
class GraphicalPasswordAuth:
 def _init_(self, master):
 self.master = master
 self.master.title("Graphical Password Authentication")
 self.master.geometry("400x300")
 self.password = "1234" # Set your password here
 self.canvas = tk.Canvas(self.master, width=400, height=300)
 self.canvas.pack()
 self.canvas.create_text(200, 50, text="Draw your password", font=("Helvetica", 
16))
 self.canvas.bind("<Button-1>", self.start_line)
 self.canvas.bind("<B1-Motion>", self.draw_line)
 self.line_start = None
 self.line_end = None
 self.user_password = ""
 def start_line(self, event):
 self.line_start = (event.x, event.y)
 def draw_line(self, event):
 if self.line_start:
 self.canvas.delete("line")
 self.line_end = (event.x, event.y)
 self.canvas.create_line(self.line_start[0], self.line_start[1], self.line_end[0], 
self.line_end[1],
 fill="blue", width=5, tags="line")
 self.line_start = self.line_end
 def authenticate_password(self):
 if self.user_password == self.password:
 messagebox.showinfo("Success", "Authentication successful!")
 else:
 messagebox.showerror("Error", "Authentication failed. Try again.")
 self.canvas.delete("line")
 self.user_password = ""
 def submit_password(self):
 self.master.bind("<Return>", lambda event: self.authenticate_password())
 def add_point(self, event):
 self.user_password += str(event.x) + "," + str(event.y) + ","
 print(self.user_password)
if _name_ == "_main_":
 root = tk.Tk()
 app = GraphicalPasswordAuth(root)
 app.submit_password()
 root.mainloop()
