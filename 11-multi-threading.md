# Using Multi-thread in python

#### app.py

```py
import threading
from camera_thread import CameraThread ## import a class
from web_thread import import run_server ## import a function here

if __name__=="__main__"
    camera1 = CameraThread()
    t1 = threading.Thread(target=camera_thread.capture_frames)
    t1.start()

    t2 = threading.Thread(target=run_server)
    t2.start()

    t1.join()
    t2.join()
```

#### camera_thread.py

```py

class CameraThread():
    def __init__():
        self.lock = threading.lock
        self.frame = None ## the frame to let others read

    def capture_frame(self):
        while(detect_stop_key()):
            ret, frame = self.cap.read()
            if ret:
                frame2 = process(frame)
                with self.lock:
                    self.frame = frame2
    def get_frame(self):
        with self.lock:
            return self.frame

```

#### web_thread.py

```py

def generate_frame():
    while True:
        frame = camera1.get_frame()
        ...
        time.sleep(30)

@app.route('/get_video_frame')
def video_frame():
    return Response(generate_frame(), mimetype....)

def run_server():
    app.run(host='0.0.0.0', ....)

```

## Concerns

### 1. How to share variable `camera1` among files?

Two ways:

1. If you have many variables to share. organize a file `globals.py` as below.

```py
#in globals.py:
camera1 = None  # This will be shared across modules
```

Then in a file e.g. in 'web_thread.py', it can access the variables like:

```py

import globals  #import the file

def generate_frame():
    while True:
        frame = globals.camera1.get_frame()  #access the global variable across files
            ...
```

### 2. Using 'lock' to ensure safe access to shared variable `frame`

```py
self.lock1 = threading.Lock() # Create a lock object

def get_frame(self):
    with self.lock1:  # Acquire the lock before reading self.frame
        return self.frame  # Return the latest frame


```

You can create more locks if you have more shared resources. ✔ Be careful of deadlocks when acquiring multiple locks at once.
