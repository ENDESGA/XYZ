<h1 align="center">ROTOR<i>MATH</i>.<span style="color: #F45;">X</span><span style="color: #3C4;">Y</span><span style="color: #57F;">Z</span></h1>

-------

# Line Animation Example

This is an example of animating lines using custom syntax in Markdown.

<canvas width="400" height="400" data-lines="[-0.5,-0.5,0.5,0.5][-0.5,0.5,0.5,-0.5][-0.8,0,0.8,0][0,-0.8,0,0.8]" data-animation="rotate" data-duration="2000"></canvas>

# Line Drawing Example

This is an example of rendering lines using HTML5 `<canvas>` within a Markdown file.

<canvas id="lineCanvas" width="400" height="400"></canvas>

### <span style="color: #888;">MATH::</span>ROTOR
A rotor efficiently represents a complete 3D rotation around the origin, using 2 components: a [vector](vectormath.xyz) and a [hangle](endesga.xyz/?page=hangle).

Unlike matrices which rotate on 3 individual planes (pitch, roll, yaw), a rotor compresses the data into a single 4-component structure; still isomorphic to a quaternion, but aligned to a +X Right, +Y Forward, +Z Up matrix orientation.

This structure also tends to perform better since it uses a lot less mathematical operations to rotate.
```glsl
#define rotor vec4
// xyz: vector, w: hangle
```
alternatively it'd be:
```glsl
struct rotor
{
  float x, y, z, w;
}
```
or
```glsl
struct rotor
{
  vec3 v;
  float a;
}
```
Whichever way, as long as the vector is first, hangle is second - to prevent mixups and mistakes.
### ALIGNMENTS:
1. **+**<span style="color: #F45;">X</span> Right, **+**<span style="color: #3C4;">Y</span> Forward, **+**<span style="color: #56F;">Z</span> Up
2. **+Pitch** tilt-up, **+Roll** clockwise, **+Yaw** turn-left
3. ***Intrinsic*** (Local): **Y**aw, then **P**itch, then **R**oll (ZXY)
### CONSTRUCTORS:
- `rotor( vector, hangle )`
- `rotor( pitch, roll, yaw )`
- `rotor( x, y, z, w )`

-------
### <span style="color: #888;">ROTOR::</span>NEW
The most minimal way to make a new rotor is with a normalized axis, and a hangle.
```glsl
rotor new_rotor( vec3 norm_axis, float hangle )
{
  return rotor( norm_axis * sin( hangle ), cos( hangle ) );
}
```
or if you only need to rotate on a specific axis, breaking it up into functions is slightly more efficient:
```glsl
rotor pitch_rotor( float hangle ) // X AXIS
{
  return rotor( sin( hangle ), 0., 0., cos( hangle ) );
}

rotor roll_rotor( float hangle ) // Y AXIS
{
  return rotor( 0., sin( hangle ), 0., cos( hangle ) );
}

rotor yaw_rotor( float hangle ) // Z AXIS
{
  return rotor( 0., 0., sin( hangle ), cos( hangle ) );
}
```

-------
### <span style="color: #888;">ROTOR::</span>MULTIPLY
To rotate one rotor by another, you multiply them.
But since a rotor is a structure, they must be multiplied in a certain way.
Every time you multiply a rotor with another, the rotation happens via the first rotor's orientation.

Rotors are Non-Commutative!
### a * b ≠ b * a
```glsl
rotor multiply_rotor( rotor a, rotor b )
{
  return rotor
  ( // this is setting xyz then w separately
    a.w * b.xyz + b.w * a.xyz - cross( a.xyz, b.xyz ),
    a.w * b.w - dot( a.xyz, b.xyz )
  );
}
```
*expanded and optimized:*
```glsl
rotor multiply_rotor( rotor a, rotor b )
{
  float a = ( q1.z + q1.x ) * ( q2.x + q2.y );
  float b = ( q1.w + q1.y ) * ( q2.w - q2.z );
  float c = ( q1.w - q1.y ) * ( q2.w + q2.z );
  float d = a + b + c;
  float e = .5 * ( ( q1.z - q1.x ) * ( q2.x - q2.y ) + d );
  return rotor
  (
    (q1.w + q1.x) * (q2.w + q2.x) + e - d,
    (q1.w - q1.x) * (q2.y + q2.z) + e - c,
    (q1.y + q1.z) * (q2.w - q2.x) + e - b,
    (q1.z - q1.y) * (q2.y - q2.z) + e - a
  );
}
```

-------
### <span style="color: #888;">ROTOR::</span>CONSTRUCT
Combining those two functions you can make a more usable PRY constructor.
Notice the order that it's multiplying. Yaw, then Pitch, then Roll. This is called an "intrinsic" rotation.

Intrinsic means "belonging to", so you can imagine the rotation happening ***to*** the rotor as it's being multiplied.
For most view matrices and typical rotations, this is common. It's clear, and makes sense from the view of the thing being rotated.
So we have the Yaw rotor, we Pitch it, then Roll it around whatever direction it was Yawed and Pitched.
```glsl
rotor pitch_roll_yaw( float pitch, float roll, float yaw )
{
  return multiply_rotor
  (
    multiply_rotor
    (
      new_rotor( vec3( 0, 0, 1 ), yaw ),
      new_rotor( vec3( 1, 0, 0 ), pitch )
    ),
    new_rotor( vec3( 0, 1, 0 ), roll )
  );
}
```
*expanded and optimized:*
```glsl
rotor pitch_roll_yaw( float pitch, float roll, float yaw )
{
  float sp = sin(pitch);
  float cp = cos(pitch);
  float sr = sin(roll);
  float cr = cos(roll);
  float sy = sin(yaw);
  float cy = cos(yaw);
  return rotor
  (
    cy * sp * cr + sy * cp * sr,
    cy * cp * sr - sy * sp * cr,
    sy * cp * cr - cy * sp * sr,
    cy * cp * cr + sy * sp * sr
  );
}
```

-------
### <span style="color: #888;">VEC3::</span>ROTATE
Finally, to rotate a point in 3D space around the origin by a rotor you can use this optimized method.
It produces the same result as the quaternion "Q.conj * V * Q", but with less operations.
```glsl
vec3 rotate( vec3 v, rotor r )
{
  vec3 c = 2. * cross( r.xyz, v );
  return v + r.w * c - cross( c, r.xyz );
}
```
*expanded and optimized:*
```glsl
vec3 rotate( vec3 v, rotor r )
{
  float a = r.y * v.z - r.z * v.y;
  float b = r.z * v.x - r.x * v.z;
  float c = r.x * v.y - r.y * v.x;
  return vec3
  (
      v.x + 2.f * (r.w * a + r.y * c - r.z * b),
      v.y + 2.f * (r.w * b + r.z * a - r.x * c),
      v.z + 2.f * (r.w * c + r.x * b - r.y * a)
  );
}
```

-------
### <span style="color: #888;">ROTOR::</span>SLERP
Blending one rotor to another isn't as simple as a lerp(), since it's using a hypersphere.
Instead you can use a Spherical Lerp, or "slerp".

This is able to rotate a rotor so it follows the shortest and most spherical path to another rotor, via some time `t` (between `0.` and `1.`).
```glsl
rotor slerp(rotor a, rotor b, float t) {
  float o = abs( dot( a, b ) );
  if(o >= .999) return normalize( a + t * ( b - a ) );
  o = acos( o );
  return normalize( sin( o - o * t ) * a + sin( o * t ) * b );
}
```
