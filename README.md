# Shor's Algorithm 

## Descripción

Este repositorio contiene material educativo sobre el **Algoritmo de Shor**, un algoritmo cuántico propuesto por Peter Shor en 1994 para la factorización de enteros. El algoritmo encuentra los factores primos de un número N con complejidad de tiempo polinomial, significativamente más rápido que los mejores algoritmos clásicos conocidos.

## Contenido

- **`Shors_Algorithm_Workshop.ipynb`**: Jupyter Notebook interactivo que cubre:
  - Aritmética modular y congruencias
  - Exponenciación modular
  - Búsqueda del período de funciones modulares
  - Cálculo de factores a partir del período
  - Introducción al circuito cuántico del algoritmo de Shor

- **`shor_247_exercise.py`**: Solución completa del ejercicio de factorización de N=247 usando a=2

- **`Requirements.txt`**: Dependencias necesarias para ejecutar el proyecto

## Instalación

1. **Clonar el repositorio** (o descargar los archivos)

2. **Instalar las dependencias**:
```bash
pip install -r Requirements.txt
```

Las dependencias incluyen:
- `matplotlib`: Para visualización de gráficas
- `numpy`: Para cálculos numéricos
- `jupyterlab`: Para ejecutar notebooks interactivos

## Uso

### Ejecutar el Notebook

Para explorar el workshop completo:

```bash
jupyter lab Shors_Algorithm_Workshop.ipynb
```

El notebook incluye ejemplos interactivos con diferentes valores de N y a:
- N=15, a=2
- N=15, a=4
- N=15, a=13
- N=371, a=2
- N=371, a=6
- N=371, a=24

### Ejecutar el Ejercicio de N=247

Para ejecutar directamente el ejercicio resuelto:

```bash
python shor_247_exercise.py
```

Este script:
1. Calcula la función f(x) = 2^x mod 247
2. Encuentra el período r de la función
3. Verifica las condiciones necesarias (r par, a^(r/2) ≢ -1 mod N)
4. Calcula los factores usando GCD
5. Genera una visualización gráfica de la función periódica

## Conceptos Clave

### Aritmética Modular

La operación módulo encuentra el residuo de una división:
- `a mod N` es el resto de dividir a entre N
- Ejemplo: `10 mod 3 = 1`

### Congruencia

Dos números a y b son congruentes módulo N si:
- `a ≡ b (mod N)` cuando `(a mod N) = (b mod N)`
- Equivalente a: `N | (a - b)` (N divide a a-b)

### Exponenciación Modular

Función clave del algoritmo: `f(x) = a^x mod N`

Esta función es periódica: existe un valor r tal que `f(x+r) = f(x)`

### Del Período a los Factores

Una vez encontrado el período r (par):

1. Sabemos que `a^r ≡ 1 (mod N)`
2. Por lo tanto: `a^r - 1 ≡ 0 (mod N)`
3. Factorizando: `(a^(r/2) + 1)(a^(r/2) - 1) ≡ 0 (mod N)`
4. Los factores se obtienen con:
   - `factor1 = GCD(a^(r/2) + 1, N)`
   - `factor2 = GCD(a^(r/2) - 1, N)`

## Ejemplo: Factorización de 247

```python
N = 247
a = 2

# El algoritmo encuentra:
# Período r = 30
# factor1 = GCD(2^15 + 1, 247) = 13
# factor2 = GCD(2^15 - 1, 247) = 19
# Verificación: 13 × 19 = 247 ✓
```

## El Circuito Cuántico

El notebook incluye información sobre el circuito cuántico que implementa el algoritmo de Shor:

**Componentes principales:**
- **H⊗m**: Compuertas Hadamard para crear superposición
- **Uf_{a,N}**: Oráculo cuántico que implementa f(x) = a^x mod N
- **QFT†**: Transformada cuántica de Fourier inversa para extraer el período

**Estados del circuito:**
- `|ψ₀⟩`: Estado inicial |0⟩⊗(m+n)
- `|ψ₁⟩`: Superposición uniforme después de Hadamard
- `|ψ₂⟩`: Estado después del oráculo modular
- `|ψ₃⟩`: Después de medir el segundo registro
- `|ψ₄⟩`: Resultado final tras QFT† y medición

## Pasos del Algoritmo de Shor

**Entrada**: Un entero positivo N

**Salida**: Un factor p de N (si existe)

1. Verificar si N es primo o potencia de primo
2. Elegir aleatoriamente a < N y calcular GCD(a, N)
3. Usar el circuito cuántico para encontrar el período r
4. Si r es impar o a^(r/2) ≡ -1 (mod N), elegir otro a
5. Calcular GCD(a^(r/2) ± 1, N) para obtener factores

## Importancia

El algoritmo de Shor representa una amenaza teórica para la criptografía RSA, que se basa en la dificultad computacional de factorizar números grandes. Si se construyen computadoras cuánticas suficientemente poderosas, RSA podría ser vulnerable.


