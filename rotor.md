<h1 align="center">ROTOR<i>MATH</i>.<span style="color: #F45;">X</span><span style="color: #3C4;">Y</span><span style="color: #57F;">Z</span></h1>

-------

<div style="position:relative;padding-top:50%;width:100%;">
  <iframe src="https://www.shadertoy.com/embed/4cdXR2?gui=true&t=0&paused=false&muted=true" style="position:absolute;top:0;left:0;width:100%;height:100%;" frameborder="0" allowfullscreen></iframe>
</div>

<iframe style="position:relative;padding-top:50%;width:100%;" src="https://www.shadertoy.com/embed/4cdXR2?gui=true&t=0&paused=false&muted=true" style="position:absolute;top:0;left:0;width:100%;height:100%;"></iframe>

## <span style="color: #777;">STRUCTURE::</span>ROTOR
A rotor efficiently represents a complete 3D rotation around the origin, using 2 components: a [vector](?page=vector) and a [hangle](?page=hangle).

<div style="display: flex; justify-content: center;">
	<svg viewBox="0 0 200 200" width="50%" fill="none" stroke="white" stroke-width="2.25" text-anchor="middle" font-size="14">
		<line x1="100" y1="100" x2="163" y2="79" stroke="#F45" opacity="0.5"/>
		<line x1="100" y1="100" x2="37" y2="79" stroke="#3C4" opacity="0.5"/>
		<ellipse cx="100" cy="100" rx="90" ry="30" stroke-dasharray="3,9" opacity="0.5"/>
		<ellipse cx="100" cy="100" rx="30" ry="20" stroke-dasharray="6,3" transform="rotate(45 100 100)"/>
		<line x1="100" y1="100" x2="100" y2="10" stroke="#56F" opacity="0.5"/>
		<line x1="100" y1="100" x2="140" y2="60"/>
		<path d="M130 60 L140 60 L140 70"/>
		<circle cx="100" cy="100" r="2" fill="white"/>
		<text x="65" y="105" fill="white" stroke="none">h</text>
		<text x="150" y="60" fill="white" stroke="none">v</text>
		<circle cx="100" cy="100" r="90"/>
	</svg>
</div>

Unlike matrices which rotate on 3 individual planes, a rotor merges the rotation into a single 4-component structure (via hyper-space); aligned to the `+X Right, +Y Forward, +Z Up` World Orientation.

This structure also tends to perform better than matrices too since it uses a lot less mathematical operations and data to rotate.

#### <span style="color: #777;">COMPONENTS:</span>
```glsl
struct rotor
{
	vec3  v; // vector
	float h; // hangle
}
```

#### <span style="color: #777;">ALIGNMENTS:</span>
- World-Space Orientation:
  - <span style="color: #F45;">+X</span> Right, <span style="color: #3C4;">+Y</span> Forward, <span style="color: #56F;">+Z</span> Up
- **+Pitch**: tilt down, **+Roll**: counterclockwise, **+Yaw**: turn right
- ***Intrinsic*** (Local): **Y**aw, then **P**itch, then **R**oll (ZXY)

*A positive rotation around any axis is always **counterclockwise** when viewed along the positive direction of that axis.*

-------
## <span style="color: #777;">ROTOR::</span>NEW
The most minimal way to make a new rotor is with a normalized vector, and a hangle.
```glsl
rotor new_rotor( vec3 norm_vec, float hangle )
{
	return rotor
	(
		norm_vec * sin( hangle ),
		cos( hangle )
	);
}
```
or if you only need to rotate on a specific axis, breaking it up into functions is slightly more efficient:
```glsl
rotor pitch_rotor( float hangle ) // X AXIS
{
	return rotor( vec3( sin( hangle ), 0., 0.), cos( hangle ) );
}

rotor roll_rotor( float hangle ) // Y AXIS
{
	return rotor( vec3( 0., sin( hangle ), 0.), cos( hangle ) );
}

rotor yaw_rotor( float hangle ) // Z AXIS
{
	return rotor( vec3( 0., 0., sin( hangle )), cos( hangle ) );
}
```

-------
## <span style="color: #777;">ROTOR::</span>LOOK
A simple and easy way to make a rotor that points in the direction from one point to another.
Since the forward-vector **is** the rotor-vector, the roll is just the hangle - so it's upright by default.
```glsl
rotor rotor_look( vec3 from, vec3 to, float roll_hangle )
{
	return new_rotor( normalize( to - from ), roll_hangle );
}
```

-------
## <span style="color: #777;">ROTOR::</span>MULTIPLY
To rotate one rotor by another, you multiply them.
But since a rotor is a structure, they must be multiplied in a certain way.
Every time you multiply a rotor with another, the rotation happens via the first rotor's orientation.

Rotors are Non-Commutative!
### a × b ≠ b × a
```glsl
rotor multiply_rotor( rotor a, rotor b )
{
	return rotor
	( // this is setting xyz then w separately
		a.h * b.v + b.h * a.v - cross( a.v, b.v ),
		a.h * b.h - dot( a.v, b.v )
	);
}
```
*expanded and optimized:*
```glsl
rotor multiply_rotor( rotor a, rotor b )
{
	float i = ( a.v.z + a.v.x ) * ( b.v.x + b.v.y );
	float j = ( a.h + a.v.y ) * ( b.h - b.v.z );
	float k = ( a.h - a.v.y ) * ( b.h + b.v.z );
	float l = i + j + k;
	float m = .5 * ( ( a.v.z - a.v.x ) * ( b.v.x - b.v.y ) + l );
	return rotor
	(
		( a.h + a.v.x ) * ( b.h + b.v.x ) + m - l,
		( a.h - a.v.x ) * ( b.v.y + b.v.z ) + m - k,
		( a.v.y + a.v.z ) * ( b.h - b.v.x ) + m - j,
		( a.v.z - a.v.y ) * ( b.v.y - b.v.z ) + m - i
	);
}
```

-------
## <span style="color: #777;">ROTOR::</span>CONSTRUCT
Combining those two functions you can make a more usable PRY constructor.
Notice the order that it's multiplying. Yaw, then Pitch, then Roll. This is called an "intrinsic" rotation.

Intrinsic means "belonging to", so you can imagine the rotation happening ***to*** the rotor as it's being multiplied.
For most view matrices and typical rotations, this is common. It's clear, and makes sense from the view of the thing being rotated.
So we have the Yaw rotor, we Pitch it, then Roll it around whatever direction it was Yawed and Pitched.
```glsl
rotor yaw_pitch_roll( float yaw, float pitch, float roll )
{
    return multiply_rotor
    (
        multiply_rotor
        (
            yaw_rotor( yaw ),
            pitch_rotor( pitch )
        ),
        roll_rotor( roll )
    );
}
```
*expanded and optimized:*
```glsl
rotor yaw_pitch_roll( float yaw, float pitch, float roll )
{
	float sy = sin( yaw );
	float cy = cos( yaw );
	float sp = sin( pitch );
	float cp = cos( pitch );
	float sr = sin( roll );
	float cr = cos( roll );
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
## <span style="color: #777;">VECTOR::</span>ROTATE
Finally, to rotate a point in 3D space around the origin by a rotor you can use this optimized method:
```glsl
vec3 rotate( vec3 v, rotor r )
{
	vec3 c = 2. * cross( r.v, v );
	return v + r.h * c - cross( c, r.v );
}
```
*expanded and optimized:*
```glsl
vec3 rotate( vec3 v, rotor r )
{
	float a = r.v.y * v.v.z - r.v.z * v.v.y;
	float b = r.v.z * v.v.x - r.v.x * v.v.z;
	float c = r.v.x * v.v.y - r.v.y * v.v.x;
	return vec3
	(
		v.v.x + 2. * ( r.h * a + r.v.y * c - r.v.z * b ),
		v.v.y + 2. * ( r.h * b + r.v.z * a - r.v.x * c ),
		v.v.z + 2. * ( r.h * c + r.v.x * b - r.v.y * a )
	);
}
```

-------
## <span style="color: #777;">ROTOR::</span>SLERP
Blending one rotor to another isn't as simple as a lerp(), since it's using a hypersphere.
Instead you can use a Spherical Lerp, or "slerp".

This is able to rotate a rotor so it follows the shortest and most spherical path to another rotor, via some time `t` (between `0.` and `1.`).
```glsl
rotor slerp( rotor a, rotor b, float t )
{
	float o = abs( dot( a, b ) );
	if(o >= .999) return normalize( a + t * ( b - a ) );
	o = acos( o );
	return normalize( sin( o - o * t ) * a + sin( o * t ) * b );
}
```
