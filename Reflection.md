#Reflection
## Comments on Update Rate

The update rate of this project appears to be tied directly to the graphic update rate.  Typically, you want your control loop to be much faster.  Initially, I start this project in an Ubuntu VM.  I was having a lot of trouble getting the car to drive at all with any PID gains even at low speed.  Then it occurred to me the both the steering angle and the debug text was updating at about 1Hz.  I decided to move to a native Ubuntu computer and the update rate improve to above 10Hz with the fasted graphic setting and slowed by a factor of about 2 with the graphic quality maxed out.  

Anyone who, has studied discrete-time (digital) control knows that a slow update kills feedback control because it introduced delay that tends to decrease the stability of control and tends to make the output oscillate more.

## Speed control
Adding a controller on speed was helpful to give the steering controller less of a moving target.  It also allow me to dial up the speed I wanted the car to drive.  The speed control was primarily PI with just a touch of D, the D control seems to make it unstable.

## Driving Speed
Increasing the car speed has a similar affect as slowing down the update rate.  As both factors cause the car to weave or oscillate more.  This makes sense because both reduce the number of updates per distance travelled causing the controller hold on to control values longer thus over correctly more and being less responsive.  On my fast computer that update over 10Hz with the fastest graphics setting I was able to successfully drive at 15MPH.  At 30MPH, the car made it around the track, but was weaving from side to side.  

##Steering Control Gains
For steering, I ended up not using any I-gain.  The I-gain will build up command by integrating error, but as the steering input is constantly changing this can be detrimental as the learned I control may be reflected what you already drove and the portion of the road you are currently driving.  I tuned the PD control by slowing increasing P and adjusting the D gain so minimize oscillation.  I believe that if the control update rate were increased, I could turn up the PD control gains and drive the track at the higher speed while staying closer to the center line and not oscillating.  But on my current computer, 15MPH is what I can do with minimal oscillation.  

## Alternative Steering Control
Typically, vehicle steering is done using either pure pursuit, the Stanley controller or model predictive control.  All of these control strategies are different, but they all have the ability to predict  and feedforward the proper steering angle based on the geometry of the desired path.  This gives all of them a distinct advantage over a pure PID controller without any feedforward.  The beauty of feedforward is that it does not affect the stability of the system.  Anyone who has ever had a feedback controls class knows that the only why to make an unstable system stable it to add feedback control.  What it seldom taught is that the converse is also true.  The only way to drive a stable system unstable is to apply feedback control.  In summary, more feedforward and less feedback would help allow this steering controller to perform better and would be less dependent on the control update rate.

