<h1 align="center">3D<i>MATH</i>.<span style="color: #F45;">X</span><span style="color: #3C4;">Y</span><span style="color: #57F;">Z</span></h1>

-------

## <span style="color: #777;">CONCEPT::</span>HANGLE

The hyper-angle ("hangle") represents a rotation around the origin in 3D space.
A `hangle` of `pi` gives a complete 3D rotation (see [CONCEPT::PI](?page=tau)), because `tau` double-covers.

It's best to make `hangle` an explicit type or macro:
```glsl
#define hangle float
```

Hangles are measured in hyper-radians ("hyrandians"):

### <div align="center">1 full rotation = π ≈ 3.14159265...</div>

<div style="display: flex; justify-content: center;">
	<svg viewBox="0 0 200 220" width="33.333%" fill="none" stroke="white" stroke-width="3" text-anchor="middle" font-size="18">
		<line x1="100" y1="100" x2="37" y2="79" stroke="#3C4" opacity="0.5"/>
		<ellipse cx="100" cy="100" rx="90" ry="30" stroke-dasharray="3,9" opacity="0.5"/>
		<ellipse cx="100" cy="100" rx="10" ry="30" transform="rotate(-30 100 100)"/>
		<ellipse cx="100" cy="100" rx="30" ry="90" stroke-dasharray="6,3" transform="rotate(-30 100 100)"/>
		<line x1="100" y1="100" x2="163" y2="79" stroke="#F45" opacity="0.5"/>
		<line x1="100" y1="100" x2="100" y2="10" stroke="#56F" opacity="0.5"/>
		<line x1="100" y1="100" x2="94.3" y2="110"/>
		<line x1="100" y1="100" x2="83" y2="130" stroke-dasharray="6,3"/>
		<circle cx="100" cy="100" r="2" fill="white"/>
		<text x="113" y="89" fill="white" stroke="none">h</text>
		<text x="100" y="215" fill="white" stroke="none">π hyradians</text>
		<circle cx="100" cy="100" r="90"/>
	</svg>
	<svg viewBox="0 0 200 220" width="33.333%" fill="none" stroke="white" stroke-width="3" text-anchor="middle" font-size="18">
		<ellipse cx="100" cy="100" rx="90" ry="30" stroke-dasharray="3,9" opacity="0.5"/>
		<line x1="100" y1="100" x2="60" y2="74" stroke-dasharray="6,3"/>
		<line x1="100" y1="100" x2="140" y2="74" stroke-dasharray="6,3"/>
		<path d="M100,100 L86.7,91.3 A50,50 0 0,1 113.3,91.3 Z"/>
		<line x1="100" y1="100" x2="163" y2="79" stroke="#F45" opacity="0.5"/>
		<line x1="100" y1="100" x2="37" y2="79" stroke="#3C4" opacity="0.5"/>
		<line x1="100" y1="100" x2="100" y2="10" stroke="#56F" opacity="0.5"/>
		<circle cx="100" cy="100" r="2" fill="white"/>
		<text x="100" y="121" fill="white" stroke="none">h</text>
		<text x="100" y="215" fill="white" stroke="none">0.63 hyradians</text>
		<circle cx="100" cy="100" r="90"/>
	</svg>
	<svg viewBox="0 0 200 220" width="33.333%" fill="none" stroke="white" stroke-width="3" text-anchor="middle" font-size="18">
		<line x1="100" y1="100" x2="163" y2="79" stroke="#F45" opacity="0.5"/>
		<ellipse cx="100" cy="100" rx="90" ry="30" stroke-dasharray="3,9" opacity="0.5"/>
		<path d="M100,100 L140,40 A100,100 0 0,1 150,123 Z" stroke-dasharray="6,3" />
		<path d="M100,100 L113.3,80 A300,100 0 0,1 116.7,107.7 Z"/>
		<line x1="100" y1="100" x2="37" y2="79" stroke="#3C4" opacity="0.5"/>
		<line x1="100" y1="100" x2="100" y2="10" stroke="#56F" opacity="0.5"/>
		<circle cx="100" cy="100" r="2" fill="white"/>
		<text x="130" y="106" fill="white" stroke="none">h</text>
		<text x="100" y="215" fill="white" stroke="none">also 0.63</text>
		<circle cx="100" cy="100" r="90"/>
	</svg>
</div>

All functions across 3dmath.xyz that have `hangle` inputs are in `hyradians`.

## <span style="color: #777;">CONCEPT::</span>DEGREES

To add a bridge between 2D and 3D rotations, `degrees` can be used to describe the same thing:
<div style="display: flex; justify-content: center; font-size: 125%;">360 degrees = τ radians = π hyradians</div>

So "rotate 90 degrees" can be inferred in 2D and 3D space easily, but result in different radian/hyradian values.

<div style="display: flex; justify-content: center;">
	<svg viewBox="0 0 500 80" width="100%" fill="none" stroke="white" stroke-width="2.25" text-anchor="middle" font-size="16">
		<text x="170" y="45" fill="white" stroke="none" font-size="100%">radians( degrees ) =</text>
		<text x="305" y="31" fill="white" stroke="none" font-size="125%">τ</text>
		<text x="325" y="32" fill="white" stroke="none" font-size="100%">×</text>
		<text x="375" y="30" fill="white" stroke="none" font-size="100%">degrees</text>
		<line x1="295" y1="40" x2="415" y2="40" stroke="white"/>
		<text x="355" y="60" fill="white" stroke="none" font-size="100%">360</text>
	</svg>
</div>
<div style="display: flex; justify-content: center;">
	<svg viewBox="0 0 500 80" width="100%" fill="none" stroke="white" stroke-width="2.25" text-anchor="middle" font-size="16">
		<text x="160" y="45" fill="white" stroke="none" font-size="100%">hyradians( degrees ) =</text>
		<text x="305" y="31" fill="white" stroke="none" font-size="125%">π</text>
		<text x="326" y="32" fill="white" stroke="none" font-size="100%">×</text>
		<text x="375" y="30" fill="white" stroke="none" font-size="100%">degrees</text>
		<line x1="295" y1="40" x2="415" y2="40" stroke="white"/>
		<text x="355" y="60" fill="white" stroke="none" font-size="100%">360</text>
	</svg>
</div>

---

*N.B. The terms "hangle" and "hyradian" are unique to 3dmath.xyz, and were created to differentiate between 2D and 3D rotations.*

-------
-------
-------

<div style="position: relative; width: 100%; height: 1.5em;">
<div style="position: absolute; left: 0;">previous</div>
<div style="position: absolute; right: 0;">next</div>
</div>
<div style="position: relative; width: 100%; height: 1.5em;">
<div style="position: absolute; left: 0;"><a href="?page=orientation">← orientation</a></div>
<div style="position: absolute; left: 50%; transform: translateX(-50%);"><a href="https://3dmath.xyz">home</a></div>
<div style="position: absolute; right: 0;"><a href="?page=vector">vector →</a></div>
</div>
