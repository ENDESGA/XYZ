<h1 align="center">MOTOR<i>MATH</i>.<span style="color: #F45;">X</span><span style="color: #3C4;">Y</span><span style="color: #57F;">Z</span></h1>

-------

## <span style="color: #777;">STRUCTURE::</span>MOTOR
A motor efficiently represents a complete 3D rotation and translation, using 2 fused [rotors](?page=rotor).

<div style="display: flex; justify-content: center;">
	<svg viewBox="0 0 300 150" width="75%" fill="none" stroke="white" stroke-width="2.25" text-anchor="middle" font-size="14">
		<line x1="200" y1="100" x2="263" y2="79" stroke="#F45" opacity="0.5"/>
		<line x1="200" y1="100" x2="137" y2="79" stroke="#3C4" opacity="0.5"/>
		<line x1="200" y1="100" x2="200" y2="10" stroke="#56F" opacity="0.5"/>
		<g transform="translate(0, 10) scale(.666)">
		<ellipse cx="100" cy="100" rx="90" ry="30" stroke-dasharray="3,9" opacity="0.5"/>
		<ellipse cx="100" cy="100" rx="30" ry="20" stroke-dasharray="6,3" transform="rotate(-45 100 100)"/>
		<line x1="100" y1="100" x2="140" y2="140"/>
		<line x1="100" y1="100" x2="300" y2="135" opacity="0.5" stroke-dasharray="6,3"/>
		<path d="M130 140 L140 140 L140 130"/>
		<circle cx="100" cy="100" r="2" fill="white"/>
		<circle cx="100" cy="100" r="90"/>
		</g>
	</svg>
</div>

It rotates, and then translates via the new rotation - it's highly ***Intrinsic***.

```glsl
struct motor
{
	rotor r; // rotation
	rotor t; // translation
};
```

-------

## <span style="color: #777;">MOTOR::</span>SHADERTOY
Click and drag the mouse around to rotate **and translate** the cube via a motor:

<div style="position:relative;padding-top:50%;width:100%;">
  <iframe src="https://www.shadertoy.com/embed/XXBBWG?gui=false&paused=true&muted=true&t=10" style="position:absolute;top:0;left:0;width:100%;height:100%;" frameborder="0"></iframe>
</div>

-------
## <span style="color: #777;">MOTOR::</span>NEW
The most minimal way to make a new motor is with a rotor and a translation vector.
```glsl
rotor rotor_halve( in rotor r )
{ // exclusive for motor creation
    return rotor( r.v * .5, r.h * .5 );
}

motor new_motor( in rotor r, in vector pos )
{
	return motor(
		rotor_halve(
			rotor_mul( r, rotor( pos, 0. ) )
		),
		r
	);
}
```

-------
## <span style="color: #777;">MOTOR::</span>INVERT
To invert the motor, which inverts both the rotation and translation, you simply invert both the rotors within:
```glsl
motor invert_motor( in motor m )
{
    return motor(
        invert_rotor( m.r ),
        invert_rotor( m.t )
    );
}
```
This function is what lead to the realization that an [observer](?page=observer) is simply an inverted motor

-------
## <span style="color: #777;">MOTOR::</span>MULTIPLY
To combine the rotation and translation of one motor with another, you multiply them.
But since a motor is a structure, they must be multiplied in a certain way.
Every time you multiply a motor with another, the rotation and translation happens via the first motor's orientation.

Motors are Non-Commutative!
### a × b ≠ b × a

```glsl
motor motor_mul( in motor a, in motor b )
{
	return motor(
		rotor_mul( a.r, b.r ),
		rotor_add(
			rotor_mul( a.r, b.t ),
			rotor_mul( a.t, b.r )
		)
	);
}
```

-------
## <span style="color: #777;">VECTOR::</span>TRANSFORM
Finally, to rotate and translate a point in 3D space by a motor you can use this method.

```glsl
vector vector_transform( in vector v, in motor m )
{
    return motor_mul(
        motor_mul(
            m,
            motor(
                rotor( vector( 0. ), 1. ),
                rotor( v, 0. )
            )
        ),
        motor(
            rotor( -m.r.v, m.r.h ),
            rotor( m.t.v, -m.t.h )
        )
    ).t.v;
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
<div style="position: absolute; left: 0;"><a href="?page=rotor">← rotor</a></div>
<div style="position: absolute; left: 50%; transform: translateX(-50%);"><a href="https://3dmath.xyz">home</a></div>
<div style="position: absolute; right: 0;"><a href="?page=observer">observer →</a></div>
</div>
