{% tikz ecb.tikz %}
\node (enc) [rectangle, draw, minimum height=2em, minimum width=2em] at (0em, 3em) {E};
\node (p) [rectangle] at (0em, 6em) {$P_i$};
\node (c) [rectangle] at (0em, 0em) {$C_i$};
\draw [->] (p.south) -- (enc.north);
\draw [->] (enc.south) -- (c.north);
{% endtikz %}
