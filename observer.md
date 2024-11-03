<h1 align="center">3D<i>MATH</i>.<span style="color: #F45;">X</span><span style="color: #3C4;">Y</span><span style="color: #57F;">Z</span></h1>

-------

## <span style="color: #777;">STRUCTURE::</span>OBSERVER
An observer has the same components as a [motor](?page=motor):
```glsl
#define observer motor
```

But is ***Inverted***.

The "position" of the observer is actually the displacement of reality from the origin, and the "look-direction" is then how reality rotates away.

Observers are **Extrinsic**.

<div style="display: flex; justify-content: center;">
	<svg viewBox="0 0 200 200" width="50%" fill="none" stroke="white" stroke-width="2.25" text-anchor="middle" font-size="14">
		<defs>
		<marker id="arrowf1" markerWidth="40" markerHeight="40" refX="20" refY="20" orient="auto" markerUnits="userSpaceOnUse">
			<path d="M15 15 L20 20 L15 25" stroke-width="2.25"/>
	    </marker>
		</defs>
		<path d="M10 100 L100 70 L190 100 L100 130 L10 100" stroke-dasharray="3,9"/>
		<line x1="100" y1="100" x2="167.5" y2="77.5" stroke="#F45"/>
		<line x1="100" y1="100" x2="32.5" y2="122.5" stroke="#F45" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="100" y1="100" x2="32.5" y2="77.5" stroke="#3C4"/>
		<line x1="100" y1="100" x2="167.5" y2="122.5" stroke="#3C4" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="100" y1="100" x2="100" y2="30" stroke="#56F"/>
		<line x1="100" y1="100" x2="100" y2="170" stroke="#56F" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="25" y1="30" x2="100" y2="100" opacity="0.25" stroke-dasharray="3,3"/>
		<line x1="25" y1="30" x2="75" y2="40" marker-end="url(#arrowf1)" opacity="0.5"/>
		<circle cx="100" cy="100" r="2" fill="white"/>
		<circle cx="25" cy="30" r="21"/>
		<ellipse cx="25" cy="30" rx="21" ry="7" stroke-dasharray="3,6" opacity="0.5"/>
	</svg>
</div>

-------

## <span style="color: #777;">OBSERVER::</span>NEW
A new observer can be made with a `from-vector` position (where it is in the world), a `to-vector` position (what it's looking at), and a `roll` hangle (`0` is upright):

```glsl
observer new_observer( in vector from_v, in vector to_v, in hangle roll )
{
    return invert_motor(
	    new_motor( look_rotor( from_v, to_v, roll ), from_v )
		);
}
```

-------

## <span style="color: #777;">VECTOR::</span>OBSERVE
Using a [projection](?page=projection), it is possible simulate an observer looking at a vector in World-Space.
The only important factor is that we're doing an **Extrinsic** multiply, which is the same as the [motor](?page=motor), but in reversed order:

```glsl
vector vector_observe( in vector world_v, in observer o, in projection p )
{
    return vector_project(
        vector_transform( world_v, o ),
        p
    );
}
```

This transforms the World-Space vector by the observer, and then projects it to View-Space for rendering straight to the screen.

-------
-------
-------

<div style="position: relative; width: 100%; height: 1.5em;">
<div style="position: absolute; left: 0;">previous</div>
<div style="position: absolute; right: 0;">next</div>
</div>
<div style="position: relative; width: 100%; height: 1.5em;">
<div style="position: absolute; left: 0;"><a href="?page=motor">← motor</a></div>
<div style="position: absolute; left: 50%; transform: translateX(-50%);"><a href="https://3dmath.xyz">home</a></div>
<div style="position: absolute; right: 0;"><a href="?page=projection">projection →</a></div>
</div>
