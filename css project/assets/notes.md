
/*new property -appearance -t's a CSS property that controls whether an element looks like a native browser/OS UI component or a custom styled one.*/
/* ============================================
   SLIDER STYLING NOTES — QuirksBlog (PPK)
   ============================================

   STRUCTURE:
   A slider = TRACK (the bar) + THUMB (the draggable circle)
   HTML: <input type="range" min="0" max="5" value="2" step="1">

   BROWSER-SPECIFIC PSEUDO-ELEMENTS:
   Thumb:
     -webkit-slider-thumb   → Chrome, Safari
     -moz-range-thumb       → Firefox
     -ms-thumb              → IE, Edge

   Track:
     -webkit-slider-runnable-track  → Chrome, Safari
     -moz-range-track               → Firefox
     -ms-track                      → IE, Edge

   NOTE: You CANNOT combine these selectors in one rule.
   Each browser ignores selectors it doesn't understand,
   so write separate rules for each.

   REQUIRED CSS TEMPLATE:
*/

input[type=range] {
    -webkit-appearance: none; /* required for Chrome/Safari */
    height: 35px;             /* set explicitly — IE/Edge hide overflow otherwise */
    padding: 0;               /* IE adds default padding — reset it */
}

input[type=range]::-webkit-slider-thumb {
    -webkit-appearance: none;
    box-sizing: content-box;  /* WebKit uses border-box by default — override it */
    /* your thumb styles */
}

input[type=range]::-moz-range-thumb {
    /* your thumb styles */
}

input[type=range]::-ms-thumb {
    /* write -ms- AFTER -webkit- so Edge uses ms values */
    /* may need different margins than other browsers */
}

input[type=range]::-webkit-slider-runnable-track {
    /* your track styles */
}

input[type=range]::-moz-range-track {
    /* your track styles */
}

input[type=range]::-ms-track {
    border-color: transparent; /* required — or IE/Edge shows native track */
    color: transparent;        /* required — same reason */
    /* your track styles */
}

/* FILLING TRACK PROGRESS (color before thumb vs after):
   Firefox and IE/Edge support this natively: */

input[type=range]::-moz-range-progress {
    background-color: #1db954; /* spotify green */
}

input[type=range]::-ms-fill-lower {
    background-color: #1db954;
}

/* Chrome/Safari have NO pseudo-element for this.
   You need JavaScript with a linear-gradient to fake it. */

/* HIDING IE/EDGE NATIVE TOOLTIP: */
input[type=range]::-ms-tooltip {
    display: none;
}

/* EVENTS TO LISTEN TO:
   Listen to BOTH 'input' and 'change' events together.
   Some browsers fire continuously while sliding,
   others only fire when sliding stops.
   Using both gives consistent cross-browser behavior. */