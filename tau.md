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
Sweeping a circle around with `pi` makes a sphere.

In **3D** space a full rotation is `pi` (see [CONCEPT::HANGLE](?page=hangle)).

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

