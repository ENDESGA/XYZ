<h1 align="center">3D<i>MATH</i>.<span style="color: #F45;">X</span><span style="color: #3C4;">Y</span><span style="color: #57F;">Z</span></h1>

-------

## <span style="color: #777;">CONCEPT::</span>DOWN
Gravity can be considered the only phenomena in this universe that has a direction: towards the most/nearest mass.

So despite an axis being a human-made abstraction, we can use the direction of gravity as a foundation for orientation: the `down` axis, where the gravity [vector](?page=vector) itself is.

<div style="display: flex; justify-content: center;">
	<svg viewBox="0 0 400 200" width="100%" fill="none" stroke="white" stroke-width="2.25" text-anchor="middle" font-size="21">
		<defs>
		<marker id="arrowa1" markerWidth="40" markerHeight="40" refX="20" refY="20" orient="auto" markerUnits="userSpaceOnUse">
			<path d="M15 15 L20 20 L15 25" stroke-width="2.25"/>
	    </marker>
	    <marker id="arrowa2" markerWidth="40" markerHeight="40" refX="20" refY="20" orient="auto" markerUnits="userSpaceOnUse">
			<path d="M10 10 L20 20 L10 30" stroke-width="4" stroke="#fff"/>
	    </marker>
		</defs>
		<circle cx="0" cy="100" r="200" opacity="0.25" stroke-dasharray="3,6"/>
		<circle cx="400" cy="100" r="100" opacity="0.25" stroke-dasharray="3,6"/>
		<circle cx="400" cy="100" r="150" opacity="0.25" stroke-dasharray="3,12"/>
		<circle cx="200" cy="100" r="5" fill="white"/>
		<line x1="200" y1="100" x2="170" y2="100" stroke-width="2.25" marker-end="url(#arrowa1)"/>
		<g transform="translate(0, 100) rotate(-25) translate(0, -100)">
		<circle cx="0" cy="100" r="150" opacity="0.25" stroke-dasharray="3,3"/>
		<circle cx="0" cy="100" r="250" opacity="0.25" stroke-dasharray="3,12"/>
		<circle cx="150" cy="100" r="5" fill="#fff" stroke="#fff"/>
		<line x1="150" y1="100" x2="110" y2="100" stroke-width="4.5" marker-end="url(#arrowa2)" stroke="#fff"/>
		</g>
		<g transform="translate(400, 100) rotate(-45) translate(-400, -100)">
		<circle cx="300" cy="100" r="5" fill="white"/>
		<line x1="300" y1="100" x2="330" y2="100" stroke-width="2.25" marker-end="url(#arrowa1)"/>
		</g>
		<g transform="translate(400, 100) rotate(-15) translate(-400, -100)">
		<circle cx="250" cy="100" r="5" fill="white"/>
		<line x1="250" y1="100" x2="270" y2="100" stroke-width="2.25" marker-end="url(#arrowa1)"/>
		</g>
		<circle cx="0" cy="100" r="90"/>
		<ellipse cx="0" cy="100" rx="90" ry="30" stroke-dasharray="3,9" opacity="0.5"/>
		<circle cx="400" cy="100" r="45"/>
		<ellipse cx="400" cy="100" rx="45" ry="15" stroke-dasharray="3,9" opacity="0.5"/>
	</svg>
</div>

Near Earth this axis points to its center of mass. However, as you approach the Moon there's a point where the gravitational influence shifts, and the axis reorients toward the Moon's center of mass instead.

## <span style="color: #777;">CONCEPT::</span>UP
Using the `down` axis as the basis, we can infer that the opposite parallel direction should be `up` - as obvious as that might be.

We can then place our reality upon the 2D-Plane that's always perpendicular to the `up`/`down` axis:

<div style="display: flex; justify-content: center;">
	<svg viewBox="0 0 200 180" width="50%" fill="none" stroke="white" stroke-width="2.25" text-anchor="middle" font-size="21">
		<defs>
		<marker id="arrowb" markerWidth="40" markerHeight="40" refX="20" refY="20" orient="auto" markerUnits="userSpaceOnUse">
			<path d="M10 10 L20 20 L10 30" stroke-width="4" stroke="#57F"/>
	    </marker>
		</defs>
		<g>
	    <text x="100" y="15" fill="#57F" stroke="none">up</text>
	    <line x1="100" y1="100" x2="145" y2="85"/>
	    <line x1="100" y1="100" x2="55" y2="115" opacity="0.5" stroke-dasharray="6,3"/>
	    <line x1="100" y1="100" x2="55" y2="85"/>
	    <line x1="100" y1="100" x2="145" y2="115" opacity="0.5" stroke-dasharray="6,3"/>
	    <line x1="100" y1="100" x2="100" y2="152" opacity="0.5" marker-end="url(#arrowa1)" stroke-width="2.25" stroke="#fff"/>
	    <path d="M10 100 L100 70 L190 100 L100 130 L10 100" stroke-dasharray="3,9"/>
	    <line x1="100" y1="100" x2="100" y2="30" stroke-width="4" marker-end="url(#arrowb)" stroke="#57F"/>
	    <circle cx="100" cy="100" r="2" fill="white"/>
		</g>
	</svg>
</div>

The 2D-Plane in which we observers stand upon is the foundational layer that everything in 3D-Space is relative to:

<div style="display: flex; justify-content: center;">
	<svg viewBox="0 0 400 200" width="100%" fill="none" stroke="white" stroke-width="2.25" text-anchor="middle" font-size="21">
    <defs>
        <marker id="ball" markerWidth="40" markerHeight="40" refX="20" refY="20" orient="auto" markerUnits="userSpaceOnUse">
            <circle cx="20" cy="20" r="2" fill="white" stroke-dasharray="0"/>
        </marker>
        <clipPath id="ellipse">
            <ellipse cx="200" cy="100" rx="200" ry="100" />
        </clipPath>
    </defs>
    <g clip-path="url(#ellipse)">
        <line x1="-70" y1="100" x2="470" y2="280" opacity="0.03125" stroke-dasharray="3,9"/>
        <line x1="470" y1="100" x2="-70" y2="280" opacity="0.03125" stroke-dasharray="3,9"/>
        <line x1="-70" y1="70" x2="470" y2="250" opacity="0.0625" stroke-dasharray="3,9"/>
        <line x1="470" y1="70" x2="-70" y2="250" opacity="0.0625" stroke-dasharray="3,9"/>
        <line x1="-70" y1="40" x2="470" y2="220" opacity="0.125" stroke-dasharray="3,9"/>
        <line x1="470" y1="40" x2="-70" y2="220" opacity="0.125" stroke-dasharray="3,9"/>
        <line x1="-70" y1="10" x2="470" y2="190" opacity="0.25" stroke-dasharray="3,9"/>
        <line x1="470" y1="10" x2="-70" y2="190" opacity="0.25" stroke-dasharray="3,9"/>
        <line x1="-70" y1="-20" x2="470" y2="160" opacity="0.125" stroke-dasharray="3,9"/>
        <line x1="470" y1="-20" x2="-70" y2="160" opacity="0.125" stroke-dasharray="3,9"/>
        <line x1="-70" y1="-50" x2="470" y2="130" opacity="0.0625" stroke-dasharray="3,9"/>
        <line x1="470" y1="-50" x2="-70" y2="130" opacity="0.0625" stroke-dasharray="3,9"/>
        <line x1="-70" y1="-80" x2="470" y2="100" opacity="0.03125" stroke-dasharray="3,9"/>
        <line x1="470" y1="-80" x2="-70" y2="100" opacity="0.03125" stroke-dasharray="3,9"/>
        <line x1="200" y1="100" x2="245" y2="85"/>
        <line x1="200" y1="100" x2="155" y2="115" opacity="0.5" stroke-dasharray="6,3"/>
        <line x1="200" y1="100" x2="155" y2="85"/>
        <line x1="200" y1="100" x2="245" y2="115" opacity="0.5" stroke-dasharray="6,3"/>
        <circle cx="230" cy="170" r="5"/>
        <line x1="230" y1="100" x2="230" y2="170" stroke-width="2.25" stroke="#777" stroke-dasharray="6,3"/>
        <line x1="110" y1="60" x2="110" y2="90" marker-end="url(#ball)" stroke-width="2.25" stroke="#777" stroke-dasharray="6,3"/>
        <path d="M110 100 L200 70 L290 100 L200 130 L110 100" stroke-dasharray="3,9"/>
        <line x1="180" y1="85" x2="180" y2="40" stroke-width="2.25" marker-end="url(#ball)" stroke="#57F" stroke-dasharray="6,3"/>
        <circle cx="200" cy="100" r="2" fill="white"/>
        <line x1="70" y1="150" x2="70" y2="90" stroke-width="2.25" stroke="#57F" stroke-dasharray="6,3"/>
        <circle cx="70" cy="90" r="21"/>
		<ellipse cx="70" cy="90" rx="21" ry="7" stroke-dasharray="3,6" opacity="0.5"/>
		<line x1="360" y1="100" x2="360" y2="70" stroke-width="2.25" stroke="#57F" stroke-dasharray="6,3"/>
        <circle cx="360" cy="70" r="9"/>
		<ellipse cx="360" cy="70" rx="9" ry="3" stroke-dasharray="3,2" opacity="0.5"/>
		<line x1="300" y1="35" x2="300" y2="60" stroke-width="2.25" stroke="#777" marker-end="url(#ball)" stroke-dasharray="6,3"/>
		<line x1="290" y1="170" x2="290" y2="150" stroke-width="2.25" marker-end="url(#ball)" stroke="#57F" stroke-dasharray="6,3"/>
    </g>
</svg>
</div>

## <span style="color: #777;">CONCEPT::</span>FORWARD
For all observers in any dimension, the default `forward` direction is always the first axis along the positive.

<div style="display: flex; justify-content: center;">
	<svg viewBox="0 0 200 200" width="33.333%" fill="none" stroke="white" stroke-width="3" text-anchor="middle" font-size="16">
		<defs>
			<marker id="arrowc" markerWidth="40" markerHeight="40" refX="20" refY="20" orient="auto" markerUnits="userSpaceOnUse">
				<path d="M15 15 L20 20 L15 25" stroke-width="2.25" stroke="#F45"/>
		    </marker>
		</defs>
		<line x1="100" y1="100" x2="170" y2="100" stroke="#F45" opacity="1.0" marker-end="url(#arrowc)"/>
		<line x1="100" y1="100" x2="30" y2="100" stroke="#F45" opacity="0.5" stroke-dasharray="6,3"/>
		<circle cx="100" cy="100" r="2" fill="white"/>
		<text x="100" y="195" fill="white" stroke="none">1 Dimension</text>
	</svg>
	<svg viewBox="0 0 200 200" width="33.333%" fill="none" stroke="white" stroke-width="3" text-anchor="middle" font-size="16">
		<line x1="100" y1="100" x2="170" y2="100" stroke="#F45" opacity="1.0" marker-end="url(#arrowc)"/>
		<line x1="100" y1="100" x2="30" y2="100" stroke="#F45" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="100" y1="100" x2="100" y2="30" stroke="#3C4" opacity="1.0"/>
		<line x1="100" y1="100" x2="100" y2="170" stroke="#3C4" opacity="0.5" stroke-dasharray="6,3"/>
		<circle cx="100" cy="100" r="2" fill="white"/>
		<text x="100" y="195" fill="white" stroke="none">2 Dimensions</text>
	</svg>
	<svg viewBox="0 0 200 200" width="33.333%" fill="none" stroke="white" stroke-width="3" text-anchor="middle" font-size="16">
		<line x1="100" y1="100" x2="167.5" y2="77.5" stroke="#F45" marker-end="url(#arrowc)"/>
		<line x1="100" y1="100" x2="32.5" y2="122.5" stroke="#F45" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="100" y1="100" x2="32.5" y2="77.5" stroke="#3C4"/>
		<line x1="100" y1="100" x2="167.5" y2="122.5" stroke="#3C4" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="100" y1="100" x2="100" y2="30" stroke="#56F"/>
		<line x1="100" y1="100" x2="100" y2="170" stroke="#56F" opacity="0.5" stroke-dasharray="6,3"/>
		<circle cx="100" cy="100" r="2" fill="white"/>
		<text x="100" y="195" fill="white" stroke="none">3 Dimensions</text>
	</svg>
</div>

Forward exists regardless of axis labels. Mathematically, unlimited dimensions are possible (e1, e2, e3, etc.), but for our 3D purposes we're going to assign <span style="color: #F45;">Forward</span> to <span style="color: #F45;">+X</span>, <span style="color: #3C4;">Left</span> to <span style="color: #3C4;">+Y</span>, and <span style="color: #56F;">Up</span> to <span style="color: #56F;">+Z</span>. These labels apply ***strictly to World-Space***, not View-Space.

The reason for this comes from how **sine** and **cosine** work. With an angle of `0`, the default result is in the <span style="color: #F45;">+X</span> direction. A positive angle rotates **counterclockwise**:

<div style="display: flex; justify-content: center;">
	<svg viewBox="0 0 200 200" width="50%" fill="none" stroke="white" stroke-width="2.25" text-anchor="middle" font-size="21">
		<path d="M150,100 A50,50 0 0,0 75,56.699" fill="none" opacity="0.5" stroke-dasharray="6,3"/>
		<path d="M125,100 A25,25 0 0,0 87.5,78.349" fill="none" marker-end="url(#arrowa1)"/>
		<line x1="100" y1="100" x2="75" y2="56.699" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="100" y1="100" x2="170" y2="100" stroke="#F45" opacity="1.0" marker-end="url(#arrowc)"/>
		<line x1="100" y1="100" x2="30" y2="100" stroke="#F45" opacity="0.5" stroke-dasharray="6,3"/>
		<line x1="100" y1="100" x2="100" y2="30" stroke="#3C4" opacity="1.0"/>
		<line x1="100" y1="100" x2="100" y2="170" stroke="#3C4" opacity="0.5" stroke-dasharray="6,3"/>
		<circle cx="100" cy="100" r="2" fill="white"/>
		<text x="132" y="52" fill="white" stroke="none" opacity="0.5">+</text>
	</svg>
	<svg viewBox="0 0 200 200" width="48%" fill="none" stroke="white" stroke-width="2.25" text-anchor="middle" font-size="16">
		<text x="19" y="81" fill="white" stroke="none" font-size="150%">y</text>
		<text x="39" y="79" fill="white" stroke="none">=</text>
		<text x="114" y="78" fill="white" stroke="none">sin( angle )</text>
		<text x="19" y="131" fill="white" stroke="none" font-size="150%">x</text>
		<text x="39" y="129" fill="white" stroke="none">=</text>
		<text x="114" y="128" fill="white" stroke="none">cos( angle )</text>
	</svg>
</div>

The [rotor](?page=rotor) structure relies on this concept: a rotor with no rotation should be facing forward - towards <span style="color: #F45;">+X</span>.

-------
-------
-------

<div style="position: relative; width: 100%; height: 1.5em;">
<div style="position: absolute; left: 0;">previous</div>
<div style="position: absolute; right: 0;">next</div>
</div>
<div style="position: relative; width: 100%; height: 1.5em;">
<div style="position: absolute; left: 0;"><a href="?page=tau">← tau</a></div>
<div style="position: absolute; left: 50%; transform: translateX(-50%);"><a href="https://3dmath.xyz">home</a></div>
<div style="position: absolute; right: 0;"><a href="?page=hangle">hangle →</a></div>
</div>
