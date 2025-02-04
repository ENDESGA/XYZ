<h1 align="center">3D<i>MATH</i>.<span style="color: #F45;">X</span><span style="color: #3C4;">Y</span><span style="color: #57F;">Z</span></h1>

-------

## <span style="color: #777;">CONCEPT::</span>TAU
Tau ( **τ** ) is the constant ratio between the circumference and radius of any circle.
Sweeping the radius around with `tau` makes a circle.

In **2D** space a full rotation is `tau`.

<div style="display: flex; justify-content: center;">
	<svg viewBox="0 0 200 200" width="50%" fill="none" stroke="white" stroke-width="2.25" text-anchor="middle" font-size="16">
		<circle cx="100" cy="100" r="2" fill="white"/>
		<line x1="100" y1="100" x2="190" y2="100"/>
		<circle cx="100" cy="100" r="90"/>
		<text x="143" y="120" fill="white" stroke="none">radius</text>
		<path id="circum" d="M 30 100 A 70 70 0 0 1 170 100" stroke="none"/>
		<text fill="white" stroke="none"><textPath href="#circum" startOffset="50%">circumference</textPath></text>
	</svg>
	<svg viewBox="0 0 200 200" width="48%" fill="none" stroke="white" stroke-width="2.25" text-anchor="middle" font-size="16">
		<text x="19" y="81" fill="white" stroke="none" font-size="150%">τ</text>
		<text x="39" y="79" fill="white" stroke="none">=</text>
		<text x="125" y="65" fill="white" stroke="none">circumference</text>
		<line x1="54" y1="75" x2="196" y2="75" stroke="white"/>
		<text x="125" y="95" fill="white" stroke="none">radius</text>
		<text x="39" y="135" fill="white" stroke="none">≈</text>
		<text x="128" y="135" fill="white" stroke="none">6.2831853072...</text>
	</svg>
</div>

Since the above method requires knowing the exact circumference and radius values, there's another way to calculate `tau` with an infinite series equation:

<div style="display: flex; justify-content: center;">
	<svg viewBox="0 0 300 100" width="100%" fill="none" stroke="white" stroke-width="3" text-anchor="middle" font-size="16">
		<text x="45" y="55" fill="white" stroke="none" font-size="150%">τ</text>
		<text x="65" y="53" fill="white" stroke="none">=</text>
		<text x="103" y="26" fill="white" stroke="none" font-size="150%">∞</text>
		<path d="M117 30 L90 30 L103.5 50 L90 70 L117 70" fill="none" stroke="white" stroke-width="2"/>
		<text x="103" y="84" fill="white" stroke="none" font-size="75%">n = 0</text>
		<text x="200" y="42" fill="white" stroke="none">16</text>
		<line x1="125" y1="50" x2="274" y2="50" stroke="white" stroke-width="1.5"/>
		<text x="200" y="69" fill="white" stroke="none">16n² + 16n + 3</text>
	</svg>
</div>

## <span style="color: #777;">CONCEPT::</span>PI
Pi ( **π** ) is half-tau: 3.14159265...

Sweeping a **2D** circle around into the third-dimension with `pi` (which in **2D** is half a rotation) makes a full sphere:

<div style="display: flex; justify-content: center;">
	<svg viewBox="0 0 200 200" width="31%" fill="none" stroke="white" stroke-width="3" text-anchor="middle" font-size="100%">
		<circle cx="100" cy="100" r="2" fill="white"/>
		<line x1="100" y1="100" x2="190" y2="100"/>
		<circle cx="100" cy="100" r="90"/>
	</svg>
	<svg viewBox="0 0 200 200" width="31%" fill="none" stroke="white" stroke-width="3" text-anchor="middle" font-size="100%">
		<ellipse cx="100" cy="100" rx="85" ry="090" stroke-dasharray="6,3" opacity="0.8"/>
		<ellipse cx="100" cy="100" rx="75" ry="090" stroke-dasharray="5,5" opacity="0.7"/>
		<ellipse cx="100" cy="100" rx="60" ry="090" stroke-dasharray="4,7" opacity="0.6"/>
		<ellipse cx="100" cy="100" rx="40" ry="090" stroke-dasharray="3,9" opacity="0.5"/>
		<circle cx="100" cy="100" r="2" fill="white"/>
		<line x1="100" y1="100" x2="139" y2="73" stroke-dasharray="6,3" opacity="0.5"/>
		<circle cx="100" cy="100" r="90"/>
	</svg>
	<svg viewBox="0 0 200 200" width="31%" fill="none" stroke="white" stroke-width="3" text-anchor="middle" font-size="100%">
		<circle cx="100" cy="100" r="2" fill="white"/>
		<ellipse cx="100" cy="100" rx="90" ry="30" stroke-dasharray="3,9" opacity="0.5"/>
		<circle cx="100" cy="100" r="90"/>
	</svg>
</div>

If it was swept with `tau` then it would double-cover, and this is reflected in how [rotors](?page=rotor) would double cover if provided with **2D** angles.

So in **3D** space, and to save halving the input angle, we can assume all angles are half - and a full 3D rotation is `pi` [hyradians](?page=hangle).

## <span style="color: #777;">TAU::</span>SINE

You can approximate cosine (then sine) via this equation, which is a tau-derived version of Bhāskara's formula:

```c
cos(x) from -τ/4 to τ/4 ≈ ((5τ² / 4) / (x² + π²)) - 4
```

Then piecing it together depending on what `x` is, you get complete `sin( x )` and `cos( x )` functions.
See one way to implement it via [this Shadertoy](https://www.shadertoy.com/view/M3jGWV):

<div style="position:relative;padding-top:50%;width:100%;">
  <iframe src="https://www.shadertoy.com/embed/M3jGWV?gui=false&paused=true&muted=true&t=10" style="position:absolute;top:0;left:0;width:100%;height:100%;" frameborder="0"></iframe>
</div>

-------
-------
-------

<div style="position: relative; width: 100%; height: 1.5em;">
<div style="position: absolute; right: 0;">next</div>
</div>
<div style="position: relative; width: 100%; height: 1.5em;">
<div style="position: absolute; left: 50%; transform: translateX(-50%);"><a href="https://3dmath.xyz">home</a></div>
<div style="position: absolute; right: 0;"><a href="?page=orientation">orientation →</a></div>
</div>
