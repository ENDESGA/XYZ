<h1 align="center">ROTOR<i>MATH</i>.<span style="color: #F45;">X</span><span style="color: #3C4;">Y</span><span style="color: #57F;">Z</span></h1>

-------

## <span style="color: #777;">STRUCTURE::</span>ROTOR
A rotor efficiently represents a rotation (from forward) in 3D space, and sits of the surface of a hypersphere. It uses 2 components: a [vector](?page=vector) and a [hangle](?page=hangle):

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

Compared to a matrix which rotates via 3 individual planes in a sequence, a rotor merges the whole rotation into a single structure.

#### <span style="color: #777;">COMPONENTS:</span>
```glsl
struct rotor
{
	vector v;
	hangle h;
};
```

#### <span style="color: #777;">ALIGNMENTS:</span>
- World-Space Orientation:
  - <span style="color: #F45;">+X</span> Forward, <span style="color: #3C4;">+Y</span> Left, <span style="color: #56F;">+Z</span> Up
- Intrinsic: **Y**aw, then **P**itch, then **R**oll (ZYX)
- While looking [forward](?page=up):
	- **+Yaw**: turns left
	- **+Pitch**: tilts down
	- **+Roll**: spins clockwise
- Uses the hangle type, since a typical angle would double-cover.

*A positive rotation around any axis is always **counterclockwise** when viewing from the positive-axis towards the rotating plane.*

<div style="display: flex; justify-content: center;">
	<svg viewBox="0 0 200 200" width="33.33333%" fill="none" stroke="white" stroke-width="2.25" text-anchor="middle" font-size="16">
		<defs>
			<marker id="arrowa1" markerWidth="40" markerHeight="40" refX="20" refY="20" orient="auto" markerUnits="userSpaceOnUse">
				<path d="M15 15 L20 20 L15 25" stroke-width="2.25"/>
		    </marker>
		</defs>
		<path d="M150,100 A50,50 0 0,0 75,56.699" fill="none" opacity="0.5" stroke-dasharray="6,3"/>
		<path d="M125,100 A25,25 0 0,0 87.5,78.349" fill="none" marker-end="url(#arrowa1)"/>
		<line x1="100" y1="100" x2="75" y2="56.699" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="100" y1="100" x2="170" y2="100" stroke="#F45" opacity="1.0" marker-end="url(#arrowc)"/>
		<line x1="100" y1="100" x2="30" y2="100" stroke="#F45" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="100" y1="100" x2="100" y2="30" stroke="#3C4" opacity="1.0"/>
		<line x1="100" y1="100" x2="100" y2="170" stroke="#3C4" opacity="0.5" stroke-dasharray="6,3"/>
		<circle cx="100" cy="100" r="4" fill="#56F" stroke="#56F"/>
		<text x="132" y="52" fill="white" stroke="none" opacity="0.5" font-size="150%">+</text>
		<text x="100" y="195" fill="white" stroke="none">yaw: XY plane</text>
	</svg>
	<svg viewBox="0 0 200 200" width="33.33333%" fill="none" stroke="white" stroke-width="2.25" text-anchor="middle" font-size="16">
		<path d="M150,100 A50,50 0 0,0 75,56.699" fill="none" opacity="0.5" stroke-dasharray="6,3"/>
		<path d="M125,100 A25,25 0 0,0 87.5,78.349" fill="none" marker-end="url(#arrowa1)"/>
		<line x1="100" y1="100" x2="75" y2="56.699" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="100" y1="100" x2="170" y2="100" stroke="#56F" opacity="1.0" marker-end="url(#arrowc)"/>
		<line x1="100" y1="100" x2="30" y2="100" stroke="#56F" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="100" y1="100" x2="100" y2="30" stroke="#F45" opacity="1.0"/>
		<line x1="100" y1="100" x2="100" y2="170" stroke="#F45" opacity="0.5" stroke-dasharray="6,3"/>
		<circle cx="100" cy="100" r="4" fill="#3C4" stroke="#3C4"/>
		<text x="132" y="52" fill="white" stroke="none" opacity="0.5" font-size="150%">+</text>
		<text x="100" y="195" fill="white" stroke="none">pitch: ZX plane</text>
	</svg>
	<svg viewBox="0 0 200 200" width="33.33333%" fill="none" stroke="white" stroke-width="2.25" text-anchor="middle" font-size="16">
		<path d="M150,100 A50,50 0 0,0 75,56.699" fill="none" opacity="0.5" stroke-dasharray="6,3"/>
		<path d="M125,100 A25,25 0 0,0 87.5,78.349" fill="none" marker-end="url(#arrowa1)"/>
		<line x1="100" y1="100" x2="75" y2="56.699" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="100" y1="100" x2="170" y2="100" stroke="#3C4" opacity="1.0" marker-end="url(#arrowc)"/>
		<line x1="100" y1="100" x2="30" y2="100" stroke="#3C4" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="100" y1="100" x2="100" y2="30" stroke="#56F" opacity="1.0"/>
		<line x1="100" y1="100" x2="100" y2="170" stroke="#56F" opacity="0.5" stroke-dasharray="6,3"/>
		<circle cx="100" cy="100" r="4" fill="#F45" stroke="#F45"/>
		<text x="132" y="52" fill="white" stroke="none" opacity="0.5" font-size="150%">+</text>
		<text x="100" y="195" fill="white" stroke="none">roll: YZ plane</text>
	</svg>
</div>

-------

## <span style="color: #777;">ROTOR::</span>SHADERTOY
Click and drag the mouse around to rotate the cube via a rotor:

<div style="position:relative;padding-top:50%;width:100%;">
  <iframe src="https://www.shadertoy.com/embed/M3jBDW?gui=false&paused=true&muted=true&t=10" style="position:absolute;top:0;left:0;width:100%;height:100%;" frameborder="0"></iframe>
</div>

(https://www.shadertoy.com/view/M3jBDW)

-------
## <span style="color: #777;">ROTOR::</span>NEW
The most minimal way to make a new rotor is with a normalized vector, and a hangle.
See what it's doing; it's turning the vector itself into a rotating object via sine and cosine:
```glsl
rotor new_rotor( in vector norm_v, in hangle h )
{
	return rotor(
		norm_v * sin( h ),
		cos( h )
	);
}
```
or if you only need to rotate on a specific axis, breaking it up into functions is slightly more efficient:
```glsl
rotor yaw_rotor( in hangle h ) // Z AXIS
{
	return rotor( vector( 0., 0., sin( h ) ), cos( h ) );
}

rotor pitch_rotor( in hangle h ) // Y AXIS
{
	return rotor( vector( 0., sin( h ), 0. ), cos( h ) );
}

rotor roll_rotor( in hangle h ) // X AXIS
{
	return rotor( vector( sin( h ), 0., 0. ), cos( h ) );
}
```

Which map to the 3 planes shown above.

-------
## <span style="color: #777;">ROTOR::</span>INVERT
Inverts the rotational direction of the rotor (used for [observers](?page=observer)):
```glsl
rotor invert_rotor( in rotor r )
{
	return rotor(
		invert_vector( r.v ),
		r.h
	);
}
```

-------
## <span style="color: #777;">ROTOR::</span>LOOK
A minimal way to make a rotor that points in the direction from one point to another. This aligns with what is stated in [CONCEPT::FORWARD](?page=orientation), where the result of `atan` (or `atan2` in other languages) gives `0` when looking <span style="color: #F45;">Forward</span> with <span style="color: #F45;">+X</span>:
```glsl
rotor look_rotor( in vector from_v, in vector to_v, in hangle roll )
{
	vector dir = vector_normalize( to_v - from_v );
	return yaw_pitch_roll(
		atan( dir.y, dir.x ) * .5,
		asin( -dir.z ) * .5,
		roll
	);
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
rotor rotor_mul( in rotor a, in rotor b )
{
	return rotor(
		a.h * b.v + b.h * a.v + vector_cross( a.v, b.v ),
		a.h * b.h - vector_dot( a.v, b.v )
	);
}
```
*expanded and optimized:*
```glsl
rotor rotor_mul( in rotor a, in rotor b )
{
	float i = ( a.v.z + a.v.x ) * ( b.v.x + b.v.y );
	float j = ( a.h + a.v.y ) * ( b.h - b.v.z );
	float k = ( a.h - a.v.y ) * ( b.h + b.v.z );
	float l = i + j + k;
	float m = .5 * ( ( a.v.z - a.v.x ) * ( b.v.x - b.v.y ) + l );
	return rotor(
		vector(
			( a.h + a.v.x ) * ( b.h + b.v.x ) + m - l,
			( a.h - a.v.x ) * ( b.v.y + b.v.z ) + m - k,
			( a.v.y + a.v.z ) * ( b.h - b.v.x ) + m - j
		),
		( a.v.z - a.v.y ) * ( b.v.y - b.v.z ) + m - i
	);
}
```

## <span style="color: #777;">ROTOR::</span>ADD
Addition is simple, but is really only used in [motor](?page=motor) code. To rotate a rotor by another, look above to `ROTOR::MULTIPLY`.
```glsl
rotor rotor_add( in rotor a, in rotor b )
{
	return rotor(
		a.v + b.v,
		a.h + b.h
	);
}
```

-------
## <span style="color: #777;">ROTOR::</span>CONSTRUCT
Combining the multiply and rotor-making functions You can create a more practical YPR constructor.
The multiplication order is Yaw, Pitch, then Roll - an "intrinsic" rotation.

Intrinsic means "inherent," so the rotation is applied to the rotor during multiplication - from its "point of view".
It's intuitive from the rotated object's perspective.
We start with the Yaw rotor, apply Pitch, then Roll:
```glsl
rotor yaw_pitch_roll( in hangle yaw, in hangle pitch, in hangle roll )
{
	return rotor_mul(
		rotor_mul(
			yaw_rotor( yaw ),
			pitch_rotor( pitch )
		),
		roll_rotor( roll )
	);
}
```
*expanded and optimized:*
```glsl
rotor yaw_pitch_roll( in hangle yaw, in hangle pitch, in hangle roll )
{
	float sy = sin( yaw );
	float cy = cos( yaw );
	float sp = sin( pitch );
	float cp = cos( pitch );
	float sr = sin( roll );
	float cr = cos( roll ); 
	return rotor(
		vector(
			sr * cp * cy - cr * sp * sy,
			cr * sp * cy + sr * cp * sy,
			cr * cp * sy - sr * sp * cy
		),
		cr * cp * cy + sr * sp * sy
	);
}
```

-------
## <span style="color: #777;">VECTOR::</span>ROTATE
Finally, to rotate a point in 3D space around the origin by a rotor you can use this method:
```glsl
vector vector_rotate( in vector v, in rotor r )
{
	vector c = 2. * vector_cross( r.v, v );
	return v + r.h * c - vector_cross( c, r.v );
}
```
*expanded and optimized:*
```glsl
vector vector_rotate( in vector v, in rotor r )
{
	float a = r.v.y * v.z - r.v.z * v.y;
	float b = r.v.z * v.x - r.v.x * v.z;
	float c = r.v.x * v.y - r.v.y * v.x;
	return vector(
		v.x + 2. * ( r.h * a + r.v.y * c - r.v.z * b ),
		v.y + 2. * ( r.h * b + r.v.z * a - r.v.x * c ),
		v.z + 2. * ( r.h * c + r.v.x * b - r.v.y * a )
	);
}
```

-------
## <span style="color: #777;">ROTOR::</span>NORMALIZE
Rotors are unit-objects, so they need to stay a constant unit size. If you're constantly making it, then it's fine. But if you have a persistent rotor that's being multiplied to and changed, then it's good to normalize it at least once before using.
This is just due to how rotors change when operated on.

We first need a function to get the magnitude:
```glsl
float rotor_magnitude( in rotor a, in rotor b )
{
    return vector_dot( a.v, b.v ) + ( a.h * b.h );
}
```
Which allows us to normalize the rotor:
```glsl
rotor rotor_normalize( in rotor r )
{
    float mag = rotor_magnitude( r, r );
    if( mag < 1e-7 ) // almost zero
    {
        return rotor( vector(0.), 1. );
    }
    float inv_mag = 1. / sqrt( mag );
    return rotor( r.v * inv_mag, r.h * inv_mag );
}
```

-------
## <span style="color: #777;">ROTOR::</span>MIX
You can very easily mix two rotors together via any lerp/mix function, but to rotate with the shorter distance we first have to check if the combined magnitude is negative; if so then invert the vector and hangle of the other rotor:
```glsl
rotor rotor_mix( in rotor a, in rotor b, in float t )
{
    float mag = rotor_magnitude( a, b );
    if( mag < 0. )
    {
	    b.v = invert_vector( b.v );
	    b.h = -b.h;
    }
    return rotor_normalize(
        rotor(
            mix( a.v, b.v, t ),
            mix( a.h, b.h, t )
        )
    );
}
```

-------
-------
-------

<div style="position: relative; width: 100%; height: 1.5em;">
<div style="position: absolute; left: 0;">previous</div>
<div style="position: absolute; right: 0;">next</div>
</div>
<div style="position: relative; width: 100%; height: 1.5em;">
<div style="position: absolute; left: 0;"><a href="?page=vector">← vector</a></div>
<div style="position: absolute; left: 50%; transform: translateX(-50%);"><a href="https://3dmath.xyz">home</a></div>
<div style="position: absolute; right: 0;"><a href="?page=motor">motor →</a></div>
</div>
