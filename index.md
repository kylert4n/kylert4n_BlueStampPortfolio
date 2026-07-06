# BlueStamp Rocket Flight Test and Data Logger
When you build a model rocket, with expensive components and hours of work, you want to have a sense of confidence before the launch, that is the purpose of my project. Some challenges I faced when building the rocket flight test and data logger were the wiring as well as the 3d design. I don't have much experience with doing wiring work nor 3d CAD so both of these tasks were challenging. My takeaway from this project is that anything is possible with enough time and effort put into it.


| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Kyler T | Monta Vista High School | Aerospace Engineering | Incoming Sophmore 

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

  # Starter Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/mfC3FOmEetY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

My starter milestone is a retro gaming handheld. I built it by soldering on multiple components onto a pcb. The build includes 2 LED dot matrix modules which serve as screens, electronic capaciter, Digitron display which help to show your score, button which helps you turn it on and off, PCB, screws, battery case, and acrylic shell. I've progressed my skills in soldering as well as general knowledge of circutry. Some challenges I faced during the assembly of the handheld was components falling out during soldering which I solved by heating up the solder and using tweazers and pushing out the solder. My plan to complete the project is to first solder all the components, prep the acrylic sheets, assemble shell, and test.




# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```c++
int motorpin1 = 2;
int motorpin2 = 3;

void setup() {
  // put your setup code here, to run once:
  pinMode(motorpin1, OUTPUT);
  
  pinMode(motorpin2, OUTPUT);
}

void loop() {
  // put your main code here, to run repeatedly:
  analogWrite(motorpin1, 0);
  analogWrite(motorpin2, 255);

}
```
```python
import tkinter as tk
import serial
import time

arduino = serial.Serial('COM3', 9600)

time.sleep(2)

def send(command):
  arduijno.write(command.encode())

window = tk.Tk()
window.title("Motor Controller")
window.geometry("300x250")

forward = tk.button(window, text="Forward"
                    command=lambda: send("F"),
                    windth=20,height=2)

reverse = tk.Button(window,text="Reverse"
                    command=lambda: send("B")
                    windth=20,height=2)

stop = tk.button(window,text="STOP",
                 command=lambda: send("S")
                 width=20,height=2)

forward.pack(pady=10)
reverse.pack(pady=10)
stop.pack(pady=10)

window.bind("<w>",lambda e: send("F"))
window.bind("<S>",lambda e: send("B"))
window.bind("<space>",lambda e: send("S"))

window.mainloop(
```

# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |

# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
