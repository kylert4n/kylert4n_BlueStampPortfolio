# BlueStamp Rocket Flight Test and Data Logger
When you build a model rocket, with expensive components and hours of work, you want to have a sense of confidence before the launch, that is the purpose of my project. Some challenges I faced when building the rocket flight test and data logger were the wiring as well as the 3d design. I don't have much experience with doing wiring work nor 3d CAD so both of these tasks were challenging. My takeaway from this project is that anything is possible with enough time and effort put into it.


| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Kyler T | Monta Vista High School | Aerospace Engineering | Incoming Sophmore 

![Headshot](/branding/KylerT.png)

  # Starter Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/mfC3FOmEetY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

My starter milestone is a retro gaming handheld. I built it by soldering on multiple components onto a pcb. The build includes 2 LED dot matrix modules which serve as screens, electronic capaciter, Digitron display which help to show your score, button which helps you turn it on and off, PCB, screws, battery case, and acrylic shell. I've progressed my skills in soldering as well as general knowledge of circutry. Some challenges I faced during the assembly of the handheld was components falling out during soldering which I solved by heating up the solder and using tweazers and pushing out the solder. My plan to complete the project is to first solder all the components, prep the acrylic sheets, assemble shell, and test.




# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

# Code
This was the first attempt at getting a response from the motor which was succesful
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
This was the first attempt at getting proper perameters set for the motor
```c++
const int ENA = 9;   // Speed (PWM)
const int IN1 = 8;   // Direction
const int IN2 = 7;

void setup() {
  pinMode(ENA, OUTPUT);
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);

  Serial.begin(9600);
}

void loop() {

  if (Serial.available()) {

    char command = Serial.read();

    if (command == 'F') {
      digitalWrite(IN1, HIGH);
      digitalWrite(IN2, LOW);
      analogWrite(ENA, 200);
    }

    else if (command == 'B') {
      digitalWrite(IN1, LOW);
      digitalWrite(IN2, HIGH);
      analogWrite(ENA, 200);
    }

    else if (command == 'S') {
      analogWrite(ENA, 0);
      digitalWrite(IN1, LOW);
      digitalWrite(IN2, LOW);
    }
  }
  
}
```
This was where I tried to get the arduino to communicate with my laptop which was an important break through for this project and is crucial for the operation of this project
```c++
void setup() {
  Serial.begin(9600);
  pinMode(LED_BUILTIN, OUTPUT);
}

void loop() {
  if (Serial.available() > 0) {
    char c = Serial.read();
    if (c == 'F') {
      Serial.println("Forward received");
      digitalWrite(LED_BUILTIN, HIGH);
    } else if (c == 'B') {
      Serial.println("Reverse received");
      digitalWrite(LED_BUILTIN, LOW);
    } else if (c == 'S') {
      Serial.println("Stop received");
    } else {
      Serial.print("Unknown: ");
      Serial.println(c);
    }
  }
}
```
This was the final iteration of the code which combines the perameters of the first iteration and the communication of the second.
```c++
// Bluetooth motor control sketch
// Commands over Serial/Bluetooth:
//   F = forward
//   B = reverse
//   S = stop
//
// This example assumes an L298N-style driver:
//   IN1 -> Arduino pin 8
//   IN2 -> Arduino pin 9
//   ENA -> Arduino pin 10 (PWM)
//
// Wiring note:
//   - Connect motor driver logic pins to these Arduino pins.
//   - Connect driver GND to Arduino GND.
//   - If using a separate motor power supply, connect its GND to Arduino GND.

const int IN1 = 8;
const int IN2 = 9;
const int ENA = 10;

void setup() {
  Serial.begin(9600);
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);
  pinMode(ENA, OUTPUT);

  digitalWrite(IN1, LOW);
  digitalWrite(IN2, LOW);
  analogWrite(ENA, 0);

  Serial.println("Bluetooth motor controller ready");
  Serial.println("Send F, B, or S");
}

void loop() {
  if (Serial.available() > 0) {
    char c = Serial.read();

    if (c == 'F' || c == 'f') {
      Serial.println("Forward");
      digitalWrite(IN1, HIGH);
      digitalWrite(IN2, LOW);
      analogWrite(ENA, 200);  // 0-255 speed
    }
    else if (c == 'B' || c == 'b') {
      Serial.println("Reverse");
      digitalWrite(IN1, LOW);
      digitalWrite(IN2, HIGH);
      analogWrite(ENA, 200);
    }
    else if (c == 'S' || c == 's') {
      Serial.println("Stop");
      digitalWrite(IN1, LOW);
      digitalWrite(IN2, LOW);
      analogWrite(ENA, 0);
    }
    else {
      Serial.print("Unknown command: ");
      Serial.println(c);
    }
  }
}
```
This was the first attempt at making a window that displays buttons which will be the main control panel
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
This was the second attempt at making a window that displays button. I tried to work on the asthetics of the window which in my opinion looks great.
```
import tkinter as tk
from tkinter import ttk, scrolledtext, messagebox
import threading
import queue
import time
import serial
from serial.tools import list_ports


class SerialGUI:
    def __init__(self, root):
        self.root = root
        root.title("Rocket Controller — Bluetooth")
        root.attributes('-fullscreen', True)
        root.configure(bg='#0f0f0f')
        root.resizable(False, False)
        # Escape to exit fullscreen
        root.bind('<Escape>', lambda e: self._exit_fullscreen())

        self.serial = None
        self.read_thread = None
        self.read_q = queue.Queue()
        self.stop_event = threading.Event()

        self.bg_canvas = tk.Canvas(self.root, bg='#0f0f0f', highlightthickness=0)
        self.bg_canvas.place(x=0, y=0, relwidth=1, relheight=1)
        self.root.bind('<Configure>', lambda e: self._draw_grid())
        self.root.after(50, self._draw_grid)

        self._build_ui()
        self._poll_serial()

    def _draw_grid(self):
        self.bg_canvas.delete('all')
        width = max(1, self.root.winfo_width())
        height = max(1, self.root.winfo_height())
        spacing = 96
        color = '#2a2a2a'
        frame_color = '#4d4d4d'

        for x in range(0, width + 1, spacing):
            self.bg_canvas.create_line(x, 0, x, height, fill=color, width=1)
        for y in range(0, height + 1, spacing):
            self.bg_canvas.create_line(0, y, width, y, fill=color, width=1)

        pad_x = 140
        pad_y = 120
        self.bg_canvas.create_rectangle(pad_x, pad_y, width - pad_x, height - pad_y, outline=frame_color, width=2)
        self.bg_canvas.create_rectangle(pad_x + 24, pad_y + 24, width - pad_x - 24, height - pad_y - 24, outline=frame_color, width=1)

    def _build_ui(self):
        # configure ttk styles for dark theme
        style = ttk.Style()
        try:
            style.theme_use('clam')
        except Exception:
            pass
        style.configure('TFrame', background='#0f0f0f')
        style.configure('TLabel', background='#0f0f0f', foreground='#f2f2f2')
        style.configure('TButton', background='#2a2a2a', foreground='#f2f2f2', font=('Segoe UI', 11, 'bold'))
        style.configure('TCombobox', fieldbackground='#161616', background='#2a2a2a', foreground='#f2f2f2')
        style.configure('TEntry', fieldbackground='#161616', foreground='#f2f2f2')

        self.status_var = tk.StringVar(value="Disconnected")
        ttk.Label(self.root, textvariable=self.status_var, foreground='#d9d9d9', background='#0f0f0f').pack(anchor="w", padx=12)

        # top area with three large colored buttons (upper half)
        top_area = tk.Frame(self.root, bg='#0f0f0f')
        top_area.pack(fill='both', expand=True)

        title_label = tk.Label(top_area, text='Controls', bg='#0f0f0f', fg='#f2f2f2', font=('Segoe UI', 30, 'bold'))
        title_label.pack(pady=(24, 10))

        center_frame = tk.Frame(top_area, bg='#0f0f0f')
        center_frame.place(relx=0.5, rely=0.25, anchor='n')

        btn_font = ("Segoe UI", 30, "bold")
        self.forward_btn = tk.Button(center_frame, text="Forward\n(F)", command=lambda: self.send_cmd('F'), bg='#1f1f1f', fg='#f2f2f2', activebackground='#3a3a3a', font=btn_font, width=14, height=3, relief='raised', bd=3)
        self.forward_btn.grid(row=0, column=0, padx=20, pady=10)

        self.reverse_btn = tk.Button(center_frame, text="Reverse\n(B)", command=lambda: self.send_cmd('B'), bg='#2b2b2b', fg='#f2f2f2', activebackground='#4a4a4a', font=btn_font, width=14, height=3, relief='raised', bd=3)
        self.reverse_btn.grid(row=0, column=1, padx=20, pady=10)

        self.stop_btn = tk.Button(center_frame, text="Stop\n(S)", command=lambda: self.send_cmd('S'), bg='#3b3b3b', fg='#f2f2f2', activebackground='#5a5a5a', font=btn_font, width=14, height=3, relief='raised', bd=3)
        self.stop_btn.grid(row=0, column=2, padx=18, pady=8)

        # small log area just above bottom controls
        self.log = scrolledtext.ScrolledText(self.root, height=6, state='disabled', wrap='word', bg='#161616', fg='#e6e6e6', insertbackground='#e6e6e6')
        self.log.pack(fill='x', padx=12, pady=(0,6))

        # bottom controls centered
        bottom_frame = tk.Frame(self.root, bg='#0f0f0f')
        bottom_frame.pack(side='bottom', fill='x', pady=24)

        controls = tk.Frame(bottom_frame, bg='#0f0f0f')
        controls.pack(anchor='center')

        self.port_var = tk.StringVar()
        ttk.Label(controls, text="Port:", style='TLabel').grid(row=0, column=0, sticky='e', padx=(0,6))
        self.port_combo = ttk.Combobox(controls, textvariable=self.port_var, width=18, state="readonly")
        self.port_combo['values'] = self._available_ports()
        self.port_combo.grid(row=0, column=1, padx=(0,12))

        ttk.Button(controls, text="Refresh", command=self._refresh_ports).grid(row=0, column=2, padx=(0,12))

        self.connect_btn = ttk.Button(controls, text="Connect", command=self.toggle_connect)
        self.connect_btn.grid(row=0, column=3, padx=(12,0))

        # key bindings
        self.root.bind('<f>', lambda e: self.send_cmd('F'))
        self.root.bind('<F>', lambda e: self.send_cmd('F'))
        self.root.bind('<b>', lambda e: self.send_cmd('B'))
        self.root.bind('<B>', lambda e: self.send_cmd('B'))
        self.root.bind('<s>', lambda e: self.send_cmd('S'))
        self.root.bind('<S>', lambda e: self.send_cmd('S'))
 
    def _exit_fullscreen(self):
        try:
            self.root.attributes('-fullscreen', False)
            self.root.geometry('1200x800')
        except Exception:
            pass

    def _available_ports(self):
        return [p.device for p in list_ports.comports()]

    def _refresh_ports(self):
        vals = self._available_ports()
        self.port_combo['values'] = vals
        if vals:
            self.port_combo.set(vals[0])
        self._log(f"Ports: {vals}")

    def toggle_connect(self):
        if self.serial and self.serial.is_open:
            self._disconnect()
        else:
            self._connect()

    def _connect(self):
        port = self.port_var.get() or (self._available_ports()[0] if self._available_ports() else None)
        if not port:
            messagebox.showwarning("No port", "No serial ports found. Connect your HC-05 and hit Refresh.")
            return
        baud = 9600
        try:
            self.serial = serial.Serial(port, baud, timeout=0.5, writeTimeout=0.5)
            self.status_var.set(f"Connected {port}@{baud}")
            self._log(f"Opened {port} @ {baud}")
            self.connect_btn.config(text='Disconnect')
            # start reader thread
            self.stop_event.clear()
            self.read_thread = threading.Thread(target=self._reader, daemon=True)
            self.read_thread.start()
        except Exception as e:
            messagebox.showerror("Connect failed", str(e))
            self._log(f"Connect error: {e}")

    def _disconnect(self):
        self.stop_event.set()
        if self.read_thread:
            self.read_thread.join(timeout=1)
        if self.serial:
            try:
                self.serial.close()
                self._log("Serial closed")
            except Exception:
                pass
        self.serial = None
        self.connect_btn.config(text='Connect')
        self.status_var.set("Disconnected")

    def _reader(self):
        while not self.stop_event.is_set():
            try:
                if self.serial and self.serial.in_waiting:
                    data = self.serial.readline().decode(errors='ignore').strip()
                    if data:
                        self.read_q.put(f"RX: {data}")
                else:
                    time.sleep(0.05)
            except Exception as e:
                self.read_q.put(f"Read error: {e}")
                break

    def _poll_serial(self):
        while not self.read_q.empty():
            line = self.read_q.get()
            self._log(line)
        self.root.after(100, self._poll_serial)

    def _log(self, text):
        self.log.configure(state='normal')
        self.log.insert('end', f"[{time.strftime('%H:%M:%S')}] {text}\n")
        self.log.see('end')
        self.log.configure(state='disabled')

    def send_cmd(self, cmd):
        if not self.serial or not self.serial.is_open:
            self._log("Serial not open — cannot send")
            return
        try:
            self.serial.write(cmd.encode())
            self.serial.flush()
            self._log(f"TX: {cmd} (button)")
        except Exception as e:
            self._log(f"Send error: {e}")

    def _manual_send(self):
        txt = self.manual_var.get()
        if not txt:
            return
        self.send_cmd(txt)


if __name__ == '__main__':
    root = tk.Tk()
    app = SerialGUI(root)
    root.mainloop()

```

# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Elagoo Arduino Uno | Program Motor | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |

# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
