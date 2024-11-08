# Godot Day/Night Cycle
Day/Night Cycle with customizable time and sky.
Available in both C# and GDScript.

By default a minute is 1 real second making a whole day be 24 real minutes long, but that can be adjusted to fit your needs (e.g. setting minute length to 60s results in real 24 hour days)

A modified version of a sky shader is included. The [original shader](https://github.com/gdquest-demos/godot-4-stylized-sky) was not made by me and uses an MIT license.

Example where the sun rises at 6 and sets at 18:

<p float="left">
   <img src="https://github.com/sventomasek/Godot-Day-Night-Cycle/blob/main/Example.gif" width="600" />
</p>

# How To Install
1. Download the latest release and extract it
2. Create a folder called 'addons' in your Godot project (must be under res://)
3. Place the 'DayNightCycle' folder into the 'addons' folder (!The location and name must be exact!)
4. Add an Environment to your scene using the three dots [like this](https://raw.githubusercontent.com/sventomasek/Godot-Day-Night-Cycle/refs/heads/main/HowTo.png)
5. On the Environment under Sky set 'Sky Material' to 'Sky_Day.tres' located in '/addons/DayNightCycle/'
6. Add a DirectionalLight3D to your scene [like this but the button on the left](https://raw.githubusercontent.com/sventomasek/Godot-Day-Night-Cycle/refs/heads/main/HowTo.png)
7. Attach the DayNightCycle script to the DirectionalLight3D ('DayNightCycle.gd' can be used with any build of Godot while 'DayNightCycle.cs' requires the .NET build)
8. With the DirectionalLight3D selected assign your WorldEnvironment to the 'World Environment' property in the inspector.
9. For the 'Night Light' property create a new DirectionalLight3D node as a child of the Sun node, set the Y rotation of it to 180 and assign it in the inspector.
10. If you run the scene now and have a Camera3D pointing forward you should see some clouds and the sun moving upward.
11. To check if the whole cycle is correct set 'Speed Multiplier' to 100

# How To Use With A Different Shader
All you have to do is remove or change some of the lines in the code (the ones that go like 'SetShaderParameter' or 'set_shader_parameter')

They're used to gradually change the shader propetries so you'll have to check the names of your shader's properties and replace them with the current ones (e.g. changing sky color from day to night).
If your shader automatically changes the colors based on the Sun's position you can probably just remove them.

# How To Get The Current Time
You can get the time by referencing the main DirectionalLight3D that has the DayNightCycle script on it and using the 'hours' and 'minutes' variables.

C# Example that will print in the HH:MM format:
```csharp
[Export] private DayNightCycle dayNightCycle;
public override void _Process(double delta)
{
   GD.Print($"{dayNightCycle.hours:D2}:{dayNightCycle.minutes:D2}");
}
```

GDScript Example that will print in the HH:MM format:
```gdscript
@export var dayNightCycle: DirectionalLight3D
func _process(delta):
   print("%02d %02d" % [dayNightCycle.hours, dayNightCycle.minutes])
```

# Customizing It
On your Sun node there's various properties that can be customized to your liking.

If you want your Sun to rise in the east you can change the 'Rotation Offset' Y to -90

Under the Time section you can change the speed multiplier which will make time go faster, while seconds per minute will change how long a minute is in real seconds.

You can also change the current time to make your scene start at a different time of day (in minutes so 480 = 8 AM).
Day length and sun rise/set hour can also be changed.

The light intensity and star intensity can be adjusted under the Lighting section.
The colors of the sky can be adjusted under the Colors section.

# Need Help?
You can contact me in my Discord server https://discord.gg/MsF7kN54T7

Just post your issue in the "tech-support" channel and I will try to help as soon as I can.
