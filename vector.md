<h1 align="center">VECTOR<i>MATH</i>.<span style="color: #F45;">X</span><span style="color: #3C4;">Y</span><span style="color: #57F;">Z</span></h1>

# Line Animation Example

This is an example of animating lines using custom syntax in Markdown.

<canvas width="400" height="400" data-lines="[-0.5,-0.5,0.5,0.5][-0.5,0.5,0.5,-0.5][-0.8,0,0.8,0][0,-0.8,0,0.8]" data-animation="rotate" data-duration="2000"></canvas>

-------

### <span style="color: #888;">MATH::</span>VECTOR
A 3 dimensional vector has 3 components.

```glsl
struct vec3
{
  float x, y, z;
}
```

-------
### <span style="color: #888;">VEC3::</span>DOT
The dot product of two vectors is a measure of how much they point in the same direction.
- If both vectors are pointing in exactly the same direction, the dot product will be a combination of magnitudes.
- If they are perpendicular (at a right angle to each other), their dot product will be zero.
- If they are pointing in opposite directions, their dot product will be a large negative value.
```glsl
float dot( vec3 a, vec3 b )
{
 return a.x * b.x + a.y * b.y + a.z * b.z;
}
```

-------
### <span style="color: #888;">VEC3::</span>LENGTH
The length of a vector is the square root of dot with itself.
```glsl
float length( vec3 v )
{
 return sqrt( dot( v, v ) );
}
```

-------
### <span style="color: #888;">VEC3::</span>NORMALIZE
Normalizing a vector scales it to have a length of 1 while preserving its direction. 
```glsl
vec3 normalize( vec3 v )
{
 float len = length( v );
 return vec3( v.x / len, v.y / len, v.z / len );
}
```

-------
### <span style="color: #888;">VEC3::</span>CROSS
The cross product of two vectors results in a new vector that is perpendicular to the other two.
```glsl
vec3 cross( vec3 a, vec3 b )
{
 return vec3(
   a.y * b.z - a.z * b.y,
   a.z * b.x - a.x * b.z,
   a.x * b.y - a.y * b.x
 );
}
```

-------
### <span style="color: #888;">VEC3::</span>LERP
Linear interpolation between two vectors based on t (between `0.` and `1.`).
```glsl
vec3 lerp( vec3 a, vec3 b, float t ) 
{
 return a + t * ( b - a );
}
```
