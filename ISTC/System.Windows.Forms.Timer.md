#   System.Windows.Forms.Timer

##  Remarks

A **Timer** is used to raise an event at user-defined intervals. This Windows timer is designed for a single-threaded environment where UI threads are used to perform processing. It requires that the user code have a UI message pump available and always operate from the same thread, or marshal the call onto another thread.

##  Examples

    public class Class1 {
        static System.Windows.Forms.Timer myTimer = new System.Windows.Forms.Timer();
        static int alarmCounter = 1;
        static bool exitFlag = false;
    
        // This is the method to run when the timer is raised.
        private static void TimerEventProcessor(Object myObject,
                                                EventArgs myEventArgs) {
           myTimer.Stop();
    
           // Displays a message box asking whether to continue running the timer.
           if(MessageBox.Show("Continue running?", "Count is: " + alarmCounter, 
              MessageBoxButtons.YesNo) == DialogResult.Yes) {
              // Restarts the timer and increments the counter.
              alarmCounter +=1;
              myTimer.Enabled = true;
           }
           else {
              // Stops the timer.
              exitFlag = true;
           }
        }
    
        public static int Main() {
           /* Adds the event and the event handler for the method that will 
              process the timer event to the timer. */
           myTimer.Tick += new EventHandler(TimerEventProcessor);
    
           // Sets the timer interval to 5 seconds.
           myTimer.Interval = 5000;
           myTimer.Start();
    
           // Runs the timer, and raises the event.
           while(exitFlag == false) {
              // Processes all the events in the queue.
              Application.DoEvents();
           }
        return 0;
        }
     }


##  Usage

1.  Double click *Toolbox* -> *Component* -> *Timer*
2.  Initiate `(Name)`, `Enabled` and `Interval` in *Property* Window.
3.  Edit the method of the `Timer.Tick` message.

(Optional)

4.  Edit `Enabled` and `Interval` wherever you like.
