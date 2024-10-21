<h1 align="center">MOTOR<i>MATH</i>.<span style="color: #F45;">X</span><span style="color: #3C4;">Y</span><span style="color: #57F;">Z</span></h1>

-------

## <span style="color: #777;">STRUCTURE::</span>MOTOR
A motor efficiently represents a complete 3D rotation and translation, using 2 fused [rotors](?page=rotor).
It rotates, and then translates via the new rotation - it's highly ***Intrinsic***.

```glsl
struct motor
{
	rotor r; // rotation
	rotor t; // translation
};
```

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
		r,
		rotor_halve(
			rotor_mul(
				r,
				rotor( vector( pos.x, pos.y, pos.z ), 0. )
			)
		)
	);
}
```

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
			rotor_mul( a.r, b.d ),
			rotor_mul( a.d, b.r )
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
			motor( rotor( vector( 0. ), 1. ), rotor( v.xyz, 0. ) )
		),
		motor( rotor( -m.r.v, m.r.h ), rotor( m.d.v, -m.d.h ) )
	).d.v;
}
```