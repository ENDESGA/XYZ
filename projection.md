<h1 align="center">PROJECTION<i>MATH</i>.<span style="color: #F45;">X</span><span style="color: #3C4;">Y</span><span style="color: #56F;">Z</span></h1>

-------

## <span style="color: #777;">CONCEPT::</span>VIEW-SPACE

A consistent 'final view' is essential, which we can get from the already-standard way pixels are stored.
This *"left-to-right, top-to-bottom"* order is also efficient since it's how most (if not all) things read/write data.

<div style="display: flex; justify-content: center;">
	<svg viewBox="0 0 200 100" width="100%" fill="none" stroke-width="1.5" text-anchor="middle" font-size="16">
		<rect x="55" y="25" width="20" height="20" fill="#777" stroke="none"/>
		<rect x="75" y="25" width="20" height="20" fill="#777" stroke="none" opacity=".625"/>
		<rect x="95" y="25" width="20" height="20" fill="#777" stroke="none" opacity=".3125"/>
		<rect x="115" y="25" width="20" height="20" fill="#777" stroke="none" opacity=".1875"/>
		<rect x="135" y="25" width="20" height="20" fill="#777" stroke="none" opacity=".0957"/>
		<rect x="155" y="25" width="20" height="20" fill="#777" stroke="none" opacity=".0390625"/>
		<rect x="55" y="45" width="20" height="20" fill="#777" stroke="none" opacity=".625"/>
		<rect x="75" y="45" width="20" height="20" fill="#777" stroke="none" opacity=".3125"/>
		<rect x="95" y="45" width="20" height="20" fill="#777" stroke="none" opacity=".1875"/>
		<rect x="115" y="45" width="20" height="20" fill="#777" stroke="none" opacity=".0957"/>
		<rect x="135" y="45" width="20" height="20" fill="#777" stroke="none" opacity=".0390625"/>
		<rect x="55" y="65" width="20" height="20" fill="#777" stroke="none" opacity=".3125"/>
		<rect x="75" y="65" width="20" height="20" fill="#777" stroke="none" opacity=".1875"/>
		<rect x="95" y="65" width="20" height="20" fill="#777" stroke="none" opacity=".0957"/>
		<rect x="115" y="65" width="20" height="20" fill="#777" stroke="none" opacity=".0390625"/>
		<line x1="55" y1="25" x2="175" y2="25" stroke="#F45"/>
		<line x1="55" y1="25" x2="55" y2="85" stroke="#3C4"/>
		<circle cx="55" cy="25" r="2" fill="white"/>
		<text x="190" y="30" fill="#F45" stroke="none">+X</text>
		<text x="55" y="100" fill="#3C4" stroke="none">+Y</text>
		<text x="100" y="9" fill="#FFF" stroke="none" font-size="10">1: Left to Right</text>
		<text x="40" y="50" fill="#FFF" stroke="none" transform="rotate(90 30,50)" font-size="10">Top to Bottom</text>
		<text x="17" y="62" fill="#FFF" stroke="none" font-size="10">2:</text>
	</svg>
	<svg viewBox="0 0 300 200" width="100%" fill="none" stroke="white" stroke-width="2.25" text-anchor="middle" font-size="16">
		<path d="M89.375 171.25 L89.375 64.375 L241.25 13.75 L241.25 118.375 Z" stroke-dasharray="3,9"/>
		<line x1="140" y1="100" x2="258.125" y2="60.625" stroke="#F45" />
		<line x1="140" y1="100" x2="72.5" y2="122.5" stroke="#F45" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="140" y1="100" x2="140" y2="30" stroke="#3C4" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="140" y1="100" x2="140" y2="170" stroke="#3C4" />
		<circle cx="140" cy="100" r="2" fill="white"/>
		<text x="270.625" y="61.625" fill="#F45" stroke="none">+X</text>
		<text x="140" y="25" fill="#3C4" opacity="0.5"   stroke="none">-Y</text>
		<text x="60" y="130.5" fill="#F45" opacity="0.5" stroke="none">-X</text>
		<text x="140" y="186" fill="#3C4" stroke="none">+Y</text>
		<!---->
		<g transform="translate(60, -10)">
		<line x1="114.6875" y1="87.1875" x2="200.3125" y2="145.625" stroke-dasharray="6,3" opacity="0.5"/>
		<line x1="114.6875" y1="125.625" x2="200.3125" y2="145.625" stroke-dasharray="6,3" opacity="0.5"/>
		<line x1="165.3125" y1="70.3125" x2="200.3125" y2="145.625" stroke-dasharray="6,3" opacity="0.5"/>
		<line x1="165.3125" y1="70.3125" x2="114.6875" y2="87.1875" stroke-dasharray="6,3"/>
		<line x1="114.6875" y1="125.625" x2="114.6875" y2="87.1875" stroke-dasharray="6,3"/>
		<line x1="114.6875" y1="125.625" x2="165.3125" y2="107.625" stroke-dasharray="3,6"/>
		<line x1="165.3125" y1="70.3125" x2="165.3125" y2="107.625" stroke-dasharray="3,6"/>
		</g>
	</svg>
</div>

The View-Space is permanently 2D, and is locked to the XY plane.

#### <span style="color: #777;">COMPONENTS:</span>
It's possible to partially simulate how the retina of the human eye works by adding some spherical nature to the projection:
```glsl
struct projection
{
    float view_scale; // from the field-of-view
    float spherical; // 0 - flat, 1 - sphere
    float sphere_scale; // 1 - full, 2 - half, inf - flat
};
```

#### <span style="color: #777;">ALIGNMENTS:</span>
- Same ordered data as images/textures
- <span style="color: #F45;">+X</span> Right, <span style="color: #3C4;">+Y</span> Down
- 2D plane in 3D World-Space

## <span style="color: #777;">PROJECTION::</span>NEW
```glsl
projection new_projection( in float fov_degrees, in float spherical, in float sphere_scale )
{
    return projection(
        1. / tan( fov_degrees * .5 ),
        spherical,
        sphere_scale
    );
}
```

## <span style="color: #777;">OPERATION::</span>REORIENTATION

Reorienting the World-Space to align with the View-Space:

<div style="display: flex; justify-content: center;">
	<svg viewBox="0 0 200 210" width="33.333%" fill="none" stroke="white" stroke-width="3" text-anchor="middle" font-size="14">
		<path d="M10 110 L100 80 L190 110 L100 140 L10 110" stroke-dasharray="3,9"/>
		<line x1="100" y1="110" x2="167.5" y2="87.5" stroke="#F45" />
		<line x1="100" y1="110" x2="32.5" y2="132.5" stroke="#F45" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="100" y1="110" x2="32.5" y2="87.5" stroke="#3C4" />
		<line x1="100" y1="110" x2="167.5" y2="132.5" stroke="#3C4" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="100" y1="110" x2="100" y2="40" stroke="#56F" />
		<line x1="100" y1="110" x2="100" y2="180" stroke="#56F" opacity="0.5" stroke-dasharray="6,3"/>
		<circle cx="100" cy="110" r="2" fill="white"/>
		<text x="180" y="88.5" fill="#F45"  stroke="none">+X</text>
		<text x="20" y="88.5" fill="#3C4"  stroke="none">+Y</text>
		<text x="100" y="35" fill="#56F"  stroke="none">+Z</text>
		<text x="20" y="140.5" fill="#F45" opacity="0.5" stroke="none">-X</text>
		<text x="180" y="140.5" fill="#3C4" opacity="0.5" stroke="none">-Y</text>
		<text x="100" y="196" fill="#56F" opacity="0.5" stroke="none">-Z</text>
		<text x="26" y="11" fill="#fff" opacity="1" stroke="none">WORLD:</text>
	</svg>
	<svg viewBox="0 0 200 210" width="33.333%" fill="none" stroke="white" stroke-width="3" text-anchor="middle" font-size="14">
		<path d="M150.625 181.25 L150.625 74.375 L49.375 40.625 L49.375 145.25 Z" stroke-dasharray="3,9"/>
		<line x1="100" y1="110" x2="167.5" y2="87.5" stroke="#56F" />
		<line x1="100" y1="110" x2="32.5" y2="132.5" stroke="#56F" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="100" y1="110" x2="32.5" y2="87.5" stroke="#F45" />
		<line x1="100" y1="110" x2="167.5" y2="132.5" stroke="#F45" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="100" y1="110" x2="100" y2="40" stroke="#3C4" />
		<line x1="100" y1="110" x2="100" y2="180" stroke="#3C4" opacity="0.5" stroke-dasharray="6,3"/>
		<circle cx="100" cy="110" r="2" fill="white"/>
		<text x="20" y="88.5" fill="#F45" stroke="none">+X</text>
		<text x="180" y="88.5" fill="#56F" stroke="none">+Z</text>
		<text x="100" y="35" fill="#3C4" stroke="none">+Y</text>
		<text x="180" y="140.5" fill="#F45" opacity="0.5" stroke="none">-X</text>
		<text x="20" y="140.5" fill="#56F" opacity="0.5" stroke="none">-Z</text>
		<text x="100" y="196" fill="#3C4" opacity="0.5" stroke="none">-Y</text>
		<text x="25" y="11" fill="#fff" opacity="1" stroke="none">CYCLE:</text>
		<text x="39.5" y="30" fill="#fff" opacity="1" stroke="none">XYZ → YZX</text>
	</svg>
	<svg viewBox="0 0 200 210" width="33.333%" fill="none" stroke="white" stroke-width="3" text-anchor="middle" font-size="14">
		<path d="M150.625 181.25 L150.625 74.375 L49.375 40.625 L49.375 145.25 Z" stroke-dasharray="3,9"/>
		<line x1="100" y1="110" x2="167.5" y2="87.5" stroke="#56F" />
		<line x1="100" y1="110" x2="32.5" y2="132.5" stroke="#56F" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="100" y1="110" x2="32.5" y2="87.5" stroke="#F45" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="100" y1="110" x2="167.5" y2="132.5" stroke="#F45" />
		<line x1="100" y1="110" x2="100" y2="40" stroke="#3C4" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="100" y1="110" x2="100" y2="180" stroke="#3C4" />
		<circle cx="100" cy="110" r="2" fill="white"/>
		<text x="20" y="88.5" fill="#F45" opacity="0.5"stroke="none">-X</text>
		<text x="180" y="88.5" fill="#56F" stroke="none">+Z</text>
		<text x="100" y="35" fill="#3C4" opacity="0.5" stroke="none">-Y</text>
		<text x="180" y="140.5" fill="#F45" stroke="none">+X</text>
		<text x="20" y="140.5" fill="#56F" opacity="0.5" stroke="none">-Z</text>
		<text x="100" y="196" fill="#3C4" stroke="none">+Y</text>
		<text x="33" y="11" fill="#fff" opacity="1" stroke="none">INVERT:</text>
		<text x="39.5" y="30" fill="#fff" opacity="1" stroke="none">XY → -XY</text>
	</svg>
</div>

```glsl
vector world_to_view( in vector v )
{
    return vector( -v.y, -v.z, v.x );
}
```

The whole idea of this is to preserve the orientation of the World-Space while using the View-Space as the 'final view', since both have equal importance for existing:
- the World-Space is intuitive for observers on a plane.
- the View-Space is intuitive for cameras/displays.

## <span style="color: #777;">VECTOR::</span>PROJECT

Projecting World-Space to View-Space:

```glsl
vector vector_project( in vector world_v, in projection p )
{
	vector pos = world_to_view( world_v );
	//pos.y = -pos.y; // uncomment if the final output is vertical-flipped
	float z = ( ( 1. - p.spherical ) * pos.z ) +
		( p.spherical * (
				vector_length(
					vector( pos.xy, pos.z * p.sphere_scale )
				) / p.sphere_scale
			)
		);
	
	return vector(
		pos.x / z * p.view_scale,
		pos.y / z * p.view_scale,
		1. / z // depth is: 1 - near, 0 - far
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
<div style="position: absolute; left: 0;"><a href="?page=observer">← observer</a></div>
<div style="position: absolute; left: 50%; transform: translateX(-50%);"><a href="https://3dmath.xyz">home</a></div>
<div style="position: absolute; right: 0;"><a href="?page=intersect">intersect →</a></div>
</div>
