<h1 align="center">MOTOR<i>MATH</i>.<span style="color: #F45;">X</span><span style="color: #3C4;">Y</span><span style="color: #57F;">Z</span></h1>

-------

### <span style="color: #888;">MATH::</span>MOTOR
A motor efficiently represents a complete 3D rotation and translation, using 2 fused [rotors](rotormath.xyz).
It rotates, and then translates via the new rotation - it's highly ***Intrinsic***.

4x4 Matrix: ***64 bytes***
Motor: ***32 bytes***

```glsl
struct motor
{
  rotor r; // rotation
  rotor t; // translation
}
```

-------
### <span style="color: #888;">MOTOR::</span>NEW
The most minimal way to make a new motor is with a rotor and a translation vector.
```glsl
motor new_motor( rotor r, vec3 t )
{
    return motor( r, multiply_rotor( r, rotor( t, 0. ) * .5 ) );
}
```

-------
### <span style="color: #888;">MOTOR::</span>MULTIPLY
To combine the rotation and translation of one motor with another, you multiply them.
But since a motor is a structure, they must be multiplied in a certain way.
Every time you multiply a motor with another, the rotation and translation happens via the first motor's orientation.

Motors are Non-Commutative!
### a * b ≠ b * a

```glsl
motor multiply_motor( motor a, motor b )
{
    return motor
    (
	    multiply_rotor( a.r, b.r ),
	    multiply_rotor( a.r, b.t ) + multiply_rotor( a.t, b.r )
	);
}
```

-------
### <span style="color: #888;">VEC3::</span>TRANSFORM
Finally, to rotate and translate a point in 3D space by a motor you can use this method.

```glsl
vec3 transform( vec3 v, motor m )
{
    return multiply_motor
    (
	    multiply_motor
	    (
		    m,
		    motor( rotor( vec3( 0. ), 1. ), rotor( v, 0. ) )
		),
        motor( rotor( -m.r.xyz, m.r.w ), vec4( m.d.xyz, -m.d.w ) )
    ).t.xyz; // return the vec3 part of the motor translation
}
```

-------
### <span style="color: #888;">MOTOR::</span>SCLERP
Blending one motor to another isn't as simple as a lerp(), since it's using a rotor and a translation vector.
Instead you can use a Screw Linear Interpolation, or "SCLERP".

This is able to rotate and translate a motor so it follows the shortest and most spherical path to another motor, via some time `t` (between `0.` and `1.`).

```glsl
motor sclerp( motor a, motor b, float t ) {
	return new_motor
	(
	  slerp( a.r, b.r, t ),
	  lerp( a.t, b.t, t )
	);
}
```
