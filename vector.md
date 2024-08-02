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
```glsl
struct vector
{
	float x;
	float y;
	float z;
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
float dot( vector a, vector b )
{
	return a.x * b.x + a.y * b.y + a.z * b.z;
}
```

## <span style="color: #777;">VECTOR::PRODUCT::</span>CROSS
The cross product of two vectors results in a new vector that is perpendicular to the other two.
```glsl
vector cross( vector a, vector b )
{
	return vector
	(
		a.y * b.z - a.z * b.y,
		a.z * b.x - a.x * b.z,
		a.x * b.y - a.y * b.x
	);
}
```


-------
## <span style="color: #777;">VECTOR::</span>LENGTH
The length of a vector is the square root of dot with itself.
```glsl
float length( vec3 v )
{
	return sqrt( dot( v, v ) );
}
```

-------
## <span style="color: #777;">VECTOR::</span>NORMALIZE
Normalizing a vector scales it to have a length of 1 while preserving its direction. 
```glsl
vec3 normalize( vec3 v )
{
	float len = length( v );
	return vec3( v.x / len, v.y / len, v.z / len );
}
```

-------

-------
## <span style="color: #777;">VECTOR::</span>LERP
Linear interpolation between two vectors based on t (between `0.` and `1.`).
```glsl
vec3 lerp( vec3 a, vec3 b, float t ) 
{
	return a + t * ( b - a );
}
```
