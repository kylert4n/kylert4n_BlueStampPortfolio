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
This was the first attempt at making a window that displays buttons
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
This was the second attempt at making a window that displays button
'''
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
        root.configure(bg='black')
        root.resizable(False, False)
        # Escape to exit fullscreen
        root.bind('<Escape>', lambda e: self._exit_fullscreen())

        self.serial = None
        self.read_thread = None
        self.read_q = queue.Queue()
        self.stop_event = threading.Event()

        self._build_ui()
        self._poll_serial()
        self.analog.write_core _//plssrq()("writebackground", "black"))

    def _build_ui(self):
        # configure ttk styles for dark theme
        style = ttk.Style()
        try:
            style.theme_use('clam')
        except Exception:
            pass
        style.configure('TFrame', background='black')
        style.configure('TLabel', background='black', foreground='white')
        style.configure('TButton', background='#222222', foreground='white')
        style.configure('TCombobox', fieldbackground='#222222', background='#222222', foreground='white')

        frm_top = ttk.Frame(self.root, padding=10, style='TFrame')
        frm_top.pack(fill="x")

        ttk.Label(frm_top, text="Port:").grid(row=0, column=0, sticky="w")
        self.port_var = tk.StringVar()
        self.port_combo = ttk.Combobox(frm_top, textvariable=self.port_var, width=18, state="readonly")
        self.port_combo['values'] = self._available_ports()
        self.port_combo.grid(row=0, column=1, padx=6)

        ttk.Button(frm_top, text="Refresh", command=self._refresh_ports).grid(row=0, column=2)

        ttk.Label(frm_top, text="Baud:").grid(row=0, column=3, sticky="w", padx=(12,0))
        self.baud_var = tk.StringVar(value="9600")
        ttk.Entry(frm_top, textvariable=self.baud_var, width=8).grid(row=0, column=4)

        self.connect_btn = ttk.Button(frm_top, text="Connect", command=self.toggle_connect)
        self.connect_btn.grid(row=0, column=5, padx=(12,0))

        self.status_var = tk.StringVar(value="Disconnected")
        ttk.Label(self.root, textvariable=self.status_var, foreground="lightblue", background='black').pack(anchor="w", padx=12)

        # top area with three large colored buttons (upper half)
        top_area = tk.Frame(self.root, bg='black')
        top_area.pack(fill='both', expand=True)

        center_frame = tk.Frame(top_area, bg='black')
        center_frame.place(relx=0.5, rely=0.25, anchor='n')

        btn_font = ("Segoe UI", 32, "bold")
        self.forward_btn = tk.Button(center_frame, text="Forward\n(F)", command=lambda: self.send_cmd('F'), bg='#28A745', fg='white', activebackground='#1f7a34', font=btn_font, width=10, height=2)
        self.forward_btn.grid(row=0, column=0, padx=18, pady=8)

        self.reverse_btn = tk.Button(center_frame, text="Reverse\n(B)", command=lambda: self.send_cmd('B'), bg='#FFC107', fg='black', activebackground='#d19b05', font=btn_font, width=10, height=2)
        self.reverse_btn.grid(row=0, column=1, padx=18, pady=8)

        self.stop_btn = tk.Button(center_frame, text="Stop\n(S)", command=lambda: self.send_cmd('S'), bg='#DC3545', fg='white', activebackground='#b42432', font=btn_font, width=10, height=2)
        self.stop_btn.grid(row=0, column=2, padx=18, pady=8)

        # small log area just above bottom controls
        self.log = scrolledtext.ScrolledText(self.root, height=6, state='disabled', wrap='word', bg='black', fg='white', insertbackground='white')
        self.log.pack(fill='x', padx=12, pady=(0,6))

        # bottom controls centered
        bottom_frame = tk.Frame(self.root, bg='black')
        bottom_frame.pack(side='bottom', fill='x', pady=24)

        controls = tk.Frame(bottom_frame, bg='black')
        controls.place(relx=0.5, rely=0.5, anchor='s')

        ttk.Label(controls, text="Port:", style='TLabel').grid(row=0, column=0, sticky='e', padx=(0,6))
        self.port_combo = ttk.Combobox(controls, textvariable=self.port_var, width=18, state="readonly")
        self.port_combo['values'] = self._available_ports()
        self.port_combo.grid(row=0, column=1, padx=(0,12))

        ttk.Button(controls, text="Refresh", command=self._refresh_ports).grid(row=0, column=2, padx=(0,12))

        ttk.Label(controls, text="Baud:", style='TLabel').grid(row=0, column=3, sticky='e', padx=(0,6))
        ttk.Entry(controls, textvariable=self.baud_var, width=8).grid(row=0, column=4)

        self.connect_btn = ttk.Button(controls, text="Connect", command=self.toggle_connect)
        self.connect_btn.grid(row=0, column=5, padx=(12,0))

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
        baud = int(self.baud_var.get())
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
'''

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
