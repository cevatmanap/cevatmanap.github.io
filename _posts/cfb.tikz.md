{% tikz cfb.tikz %}
\tikzset{
  pics/xor/.style args={#1, #2}{
     code={
       \node (#1) [circle, draw, minimum width=#2] at (0,0) {};
       \draw [-] (#1.south)--(#1.north);
       \draw [-] (#1.east)--(#1.west);
     }
  }
}
\tikzset{
  pics/feed/.style args={#1, #2}{
     code={
       \draw [->] (0,0) -- (#1 / 2,0) -- (#1 / 2, #2) -- (#1,#2);
     }
  }
}



\node (enc0) [rectangle, draw, minimum height=2em, minimum width=2em] at (2em, 3em) {E};
\draw (2em, 5em) pic{xor={xor0, 1em}};
\node (iv) [rectangle] at (0em, 5em) {$IV$};
\node (p0) [rectangle] at (2em, 7em) {$P_0$};
\node (c0) [rectangle] at (2em, 0em) {$C_0$};
\draw [->] (p0.south) -- (xor0.north);
\draw [->] (iv.east) -- (xor0.west);
\draw [->] (xor0.south) -- (enc0.north);
\draw [->] (enc0.south) -- (c0.north);
\draw (2em, 1.5em) pic{feed={3em, 3.5em}};

\def\x{3.5em}
\node (enc1) [rectangle, draw, minimum height=2em, minimum width=2em] at (2em+\x, 3em) {E};
\draw (2em+\x, 5em) pic{xor={xor1, 1em}};
%\node (iv) [rectangle] at (0em, 5em) {$IV$};
\node (p1) [rectangle] at (2em+\x, 7em) {$P_1$};
\node (c1) [rectangle] at (2em+\x, 0em) {$C_1$};
\draw [->] (p1.south) -- (xor1.north);
%\draw [->] (iv.east) -- (xor1.west);
\draw [->] (xor1.south) -- (enc1.north);
\draw [->] (enc1.south) -- (c1.north);
\draw (2em+\x, 1.5em) pic{feed={3em, 3.5em}};

\node (dots) [rectangle] at (2em + \x + 3.5em, 3em) {$\dots$};

\def\x{3.5em+7.5em}
\node (enci) [rectangle, draw, minimum height=2em, minimum width=2em] at (2em+\x, 3em) {E};
\draw (2em+\x, 5em) pic{xor={xori, 1em}};
%\node (iv) [rectangle] at (0em, 5em) {$IV$};
\node (pi) [rectangle] at (2em+\x, 7em) {$P_i$};
\node (ci) [rectangle] at (2em+\x, 0em) {$C_i$};
\draw [->] (pi.south) -- (xori.north);
%\draw [->] (iv.east) -- (xor1.west);
\draw [->] (xori.south) -- (enci.north);
\draw [->] (enci.south) -- (ci.north);
\draw (2em+\x, 1.5em) pic{feed={3em, 3.5em}};


\draw (2em+\x-3.5em, 1.5em) pic{feed={3em, 3.5em}};

\node (dots) [rectangle] at (2em + \x + 3.5em, 3em) {$\dots$};

\def\x{3.5em + 15em}

\node (encn) [rectangle, draw, minimum height=2em, minimum width=2em] at (2em+\x, 3em) {E};
\draw (2em+\x, 5em) pic{xor={xorn, 1em}};
%\node (iv) [rectangle] at (0em, 5em) {$IV$};
\node (pn) [rectangle] at (2em+\x, 7em) {$P_{n-1}$};
\node (cn) [rectangle] at (2em+\x, 0em) {$C_{n-1}$};
\draw [->] (pn.south) -- (xorn.north);
%\draw [->] (iv.east) -- (xor1.west);
\draw [->] (xorn.south) -- (encn.north);
\draw [->] (encn.south) -- (cn.north);

\draw (2em+\x-3.5em, 1.5em) pic{feed={3em, 3.5em}};

{% endtikz %}
