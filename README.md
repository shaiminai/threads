# threads
import threading
import time
import os
import shutil

lock = threading.Lock()

def dots():
    while True:
        with lock:
            print("...")
        time.sleep(0.01)

def files():
    src = r"C:\Users\shaim\Documents\filess"
    dst = r"C:\Users\shaim\Documents\files"
    back_slash = r"\\"

    list_of_files = os.listdir(src) # returns a list containing the names of the entries in the directory given by path.

    while len(os.listdir(src)) > 0:
       # with lock:  # if there were other functions which use the same files it won't work properly
            for file in list_of_files:
                shutil.move(src + back_slash + file, dst)
                with lock:
                    print(file + " was transferred")
    print("Transfer Finished")


t1 = threading.Thread(target=files)
t2 = threading.Thread(target=dots)
t1.start()
t2.start()
