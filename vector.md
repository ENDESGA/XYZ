<h1 align="center">VECTOR<i>MATH</i>.<span style="color: #F45;">X</span><span style="color: #3C4;">Y</span><span style="color: #57F;">Z</span></h1>

-------

## <span style="color: #777;">STRUCTURE::</span>VECTOR
A vector has 3 components that represent each spatial-axis.

<div style="display: flex; justify-content: center;">
	<svg viewBox="0 0 200 200" width="50%" fill="none" stroke="white" stroke-width="2.25" text-anchor="middle" font-size="14">
		<path d="M10 100 L100 70 L190 100 L100 130 L10 100" stroke-dasharray="3,9"/>
		<line x1="100" y1="100" x2="167.5" y2="77.5" stroke="#F45"/>
		<line x1="100" y1="100" x2="32.5" y2="122.5" stroke="#F45" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="100" y1="100" x2="32.5" y2="77.5" stroke="#3C4"/>
		<line x1="100" y1="100" x2="167.5" y2="122.5" stroke="#3C4" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="100" y1="100" x2="100" y2="30" stroke="#56F"/>
		<line x1="100" y1="100" x2="100" y2="170" stroke="#56F" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="100" y1="100" x2="140" y2="60"/>
		<path d="M130 60 L140 60 L140 70"/>
		<circle cx="100" cy="100" r="2" fill="white"/>
		<text x="152" y="52" fill="white" stroke="none">xyz</text>
		<text x="180" y="78.5" fill="#F45" stroke="none">+X</text>
		<text x="20" y="78.5" fill="#3C4" stroke="none">+Y</text>
		<text x="100" y="25" fill="#56F" stroke="none">+Z</text>
		<text x="20" y="130.5" fill="#F45" opacity="0.5" stroke="none">-X</text>
		<text x="180" y="130.5" fill="#3C4" opacity="0.5" stroke="none">-Y</text>
		<text x="100" y="186" fill="#56F" opacity="0.5" stroke="none">-Z</text>
	</svg>
</div>

#### <span style="color: #777;">COMPONENTS:</span>

```c
struct vector
{
	float x;
	float y;
	float z;
};
```

Though in the example code (which is in GLSL) it's treating `vector` as a `vec3` via a macro:
```glsl
#define vector vec3
```

-------
## <span style="color: #777;">VECTOR::</span>MATH
Operate with a `vector`, with `[operation]` being `add +`, `sub -`, `mul *`, or `div /`:

```glsl
float vector_[operation]( in vector a, in vector b )
{
	return vector(
		a.x [operation] b.x,
		a.y [operation] b.y,
		a.z [operation] b.z
	);
}
```
and if it's operating with a single float value:
```glsl
float vector_[operation]_float( in vector v, in float n )
{
	return vector(
		v.x [operation] n,
		v.y [operation] n,
		v.z [operation] n
	);
}
```

In languages like GLSL these functions are built into types like `vec3`. But in languages like C there's no overhead, so this is required.

-------
## <span style="color: #777;">VECTOR::</span>INVERT
<div style="display: flex; justify-content: center;">
	<svg viewBox="0 0 200 180" width="50%" fill="none" stroke="white" stroke-width="2.25" text-anchor="middle" font-size="14">
		<path d="M10 90 L100 60 L190 90 L100 120 L10 90" stroke-dasharray="3,9"/>
		<line x1="100" y1="90" x2="167.5" y2="67.5" stroke="#F45"/>
		<line x1="100" y1="90" x2="32.5" y2="112.5" stroke="#F45" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="100" y1="90" x2="32.5" y2="67.5" stroke="#3C4"/>
		<line x1="100" y1="90" x2="167.5" y2="112.5" stroke="#3C4" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="100" y1="90" x2="100" y2="20" stroke="#56F"/>
		<line x1="100" y1="90" x2="100" y2="160" stroke="#56F" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="100" y1="90" x2="140" y2="50" stroke="#777"/>
		<path d="M130 50 L140 50 L140 60" stroke="#777"/>
		<line x1="100" y1="90" x2="60" y2="130"/>
		<path d="M70 130 L60 130 L60 120"/>
		<circle cx="100" cy="90" r="2" fill="white"/>
		<text x="152" y="37" fill="#777" stroke="none">x y z</text>
		<text x="45" y="148" fill="white" stroke="none">-x -y -z</text>
	</svg>
</div>
To get a vector that's pointing in the opposite direction, you can simply invert the components:

```glsl
vector invert_vector( in vector v )
{
	return vector(
		-a.x,
		-a.y,
		-a.z
	);
}
```

-------
## <span style="color: #777;">VECTOR::</span>PRODUCT
A "product" is the result of a particular fusion of two vectors.
## <span style="color: #777;">VECTOR::PRODUCT::</span>DOT
The dot product of two vectors is how much they point in the same direction.
- If both vectors are pointing in exactly the same direction, the dot product will be **positive**.
- If both vectors are perpendicular (at a right angle), the dot product will be **zero**.
- If both vectors are pointing in opposite directions, their dot product will be **negative**.
```glsl
float vector_dot( in vector a, in vector b )
{
	return a.x * b.x + a.y * b.y + a.z * b.z;
}
```

## <span style="color: #777;">VECTOR::PRODUCT::</span>CROSS
The cross product of two vectors results in a new vector that is perpendicular to the other two.
```glsl
vector vector_cross( in vector a, in vector b )
{
	return vector(
		a.y * b.z - a.z * b.y,
		a.z * b.x - a.x * b.z,
		a.x * b.y - a.y * b.x
	);
}
```


-------
## <span style="color: #777;">VECTOR::</span>LENGTH
The length of a vector is the square root of the dot product with itself:
```glsl
float vector_length( in vector v )
{
	return sqrt( vector_dot( v, v ) );
}
```

-------
## <span style="color: #777;">VECTOR::</span>NORMALIZE
Normalizing a vector scales it to have a length of 1 while preserving its direction. 
```glsl
vector vector_normalize( in vector v )
{
	float l = vector_length( v );
	return vector(
		v.x / l,
		v.y / l,
		v.z / l
	);
}
```

-------

-------
## <span style="color: #777;">VECTOR::</span>LERP
Linear interpolation between two vectors based on t (between `0.` and `1.`).
```glsl
vector vector_lerp( in vector a, in vector b, in float t ) 
{
	return a + t * ( b - a );
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
<div style="position: absolute; left: 0;"><a href="?page=hangle">← hangle</a></div>
<div style="position: absolute; left: 50%; transform: translateX(-50%);"><a href="https://3dmath.xyz">home</a></div>
<div style="position: absolute; right: 0;"><a href="?page=rotor">rotor →</a></div>
</div>
