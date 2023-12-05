### Formula for sum of numbers from 2 to n
$$
\sum_{i=2}^ni=\frac{n(n+1)}{2}-1
$$

### Formula for sum of numbers one less than the natural series starting at 2
$$
\sum_{i=2}^n(i-1)=\frac{n(n-1)}{2}
$$

### Formula for sum of $2^n$ from 0 to n
$$
\sum_{i=0}^n2^n=2n-1
$$

### Formula for sum of $2^n$ from 1 to n
$$
\sum_{i=1}^n2^n=2n-2
$$

### Formula for $\sum_{i=0}^\infty kx^k$
$$
\sum_{i=0}^\infty kx^k=\frac{x}{(1-x)²}
$$

### Masterteoremet
- Bruker rekurrens på form $T(n)=aT(n/b)+f(n)$
    - $a$: antall delproblemer
    - $n/b$: størrelse på delproblemene
    - $f(n)$: tid til oppdeling og kombinasjon 
    - $a\geq 1$, $b>1$ er konstanter, $f(n)$ er asymptotisk positiv funksjon
- Scenarioer:
    1. $f(n)=O(n^{\log_b(a-\epsilon)})$ for konstant $\epsilon>0 \to T(n)=\theta(n^{\log_b(a)})$
    2. $f(n)=\theta(n^{\log_b(a)}\cdot\log^k(n)) \to T(n)=\theta(n^{\log_b(a)}\log(n))=\theta(f(n)\log(n))$
    3. $f(n)=\Omega(n^{\log_b(a+\epsilon)})$ for konstant $\epsilon>0$ og tilstrekkelig stor $n \to T(n)=\theta(f(n))$
 
### Substitusjonsmetoden


### Rekursjonstremetoden


### Binærsøk


### Hashfunksjoner