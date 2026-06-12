---

categories: Houdini

tags:

- note

- Houdini

- Vex

date: 2026-06-09

---

  

# Delete By Distance

  

```c

// 1. Define your threshold distance

float threshold = chf("distance_threshold");

  

// 2. Initialize variables to store results from xyzdist

int prim;

vector uv;

  

// 3. Find the distance to the closest location on Input 1

float dist = xyzdist(1, @P, prim, uv);

  

// 4. Delete the point if it's too close

if (dist < threshold) {

removepoint(0, @ptnum);

}

```

  

# HSCRIPT - Setup Focus Distance

  

```c

vlength(vtorigin(".", "../null1"))

```

  

# Preview Shader

  

```c

@gl_spherepoints = 1;

```

  
  

# Additive Particle Shader

  

```c

// Frist Node connect to the camera position

vector camP = point(1, "P", 0);

  

@P = normalize(@P - camP) + camP;

  
  

// New Wranngle attribute Find Near Points

  

float distance = chf("distance");

int maxpts = chf("maxpts");

  

int nearpts[] = nearpoints(0,@P,distance,maxpts);

  

int numNearPts = len(nearpts);

  

f@glow = (float(numNearPts) - 1) / (maxpts - 1);

  

```

  
  

# Fetch Noise

  

```c

// 1. Get the class of the current point

int myClass = i@class;

  

// 2. Search Input 1 for the first point that matches this class

// findattribval(input, type, attribute_name, value)

int targetPt = findattribval(1, "point", "class", myClass);

  

// 3. If a match was found (returns -1 if no match)

if (targetPt != -1) {

// Example: Grab the position of that matching point

float targetNoise = point(1, "noise", targetPt);

@tbvis = targetNoise;

}

```

  
  

# 90 Rotation

  

```c

int noise = rint(fit01(rand(@class+chi("Seed")), 0, 10));

  
  

@up = set(0,0,1);

  

v@N = set(0,1,0);

  

p@orient = quaternion(maketransform(@N, @up));

  
  

float angle = noise * 90;

vector axis = set(0,1,0);

vector4 rotation = quaternion(angle, axis);

p@orient = qmultiply(p@orient, rotation);

```

  
  

# QUATERNION ROTATION

  

```c

@up = set(0,1,0);

  

v@N = normalize(vector(rand(@ptnum)) - 0.5);

  

p@orient = quaternion(maketransform(@N, @up));

  
  

// Rotate the point by 90 degrees around the z-axis

float angle = 90;

vector axis = set(0,0,1);

vector4 rotation = quaternion(angle, axis);

p@orient = qmultiply(p@orient, rotation);

  

```

  

# FIND CLASS:

  

```c

// 1. Get the class of the current point

int myClass = i@class;

  

// 2. Search Input 1 for the first point that matches this class

// findattribval(input, type, attribute_name, value)

int targetPt = findattribval(1, "point", "class", myClass);

  

// 3. If a match was found (returns -1 if no match)

if (targetPt != -1) {

// Example: Grab the position of that matching point

vector targetPos = point(1, "P", targetPt);

// Do something with it, like creating a line or moving the point

@P = targetPos;

}

```

  
  

# FADE POINTS:

  

```c

// Controls

float duration = chf("duration"); // How long the fade takes (in frames)

float start_delay = chf("start_delay"); // Global offset to start the whole effect

  

// Attributes

// Assume @noise is a value between 0 and 1

// We multiply it by a 'spread' factor to stagger the start times

float noise_offset = @noise * chf("noise_spread");

float currentTime = @Frame;

  

// The point starts fading at (start_delay + noise_offset)

// The point finishes fading at (start_delay + noise_offset + duration)

float start = start_delay + noise_offset;

float end = start + duration;

  

// Fade in attribute

float fade = smooth(start, end, currentTime);

  

@tbfoff = clamp(fade, 0, 1);

```