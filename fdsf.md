¡Claro! Aquí tienes un informe sobre los métodos de ordenamiento en vectores en Python con ejemplos de código: 

  

--- 

  

# Métodos de Ordenamiento en Vectores (Python) 

  

## 1. Introducción 

  

El ordenamiento es una operación fundamental que organiza los elementos de una lista en un orden específico. Los métodos de ordenamiento se dividen en dos categorías principales: elementales y no elementales. 

  

## 2. Métodos de Ordenamiento Elementales 

  

### 2.1. Ordenamiento por Inserción 

  

**Definición:** El ordenamiento por inserción construye el vector ordenado uno a uno, colocando cada elemento en su posición correcta. 

  

**Sintaxis/Estructura:** 

  

```python 

def insertion_sort(array): 

    for i in range(1, len(array)): 

        key = array[i] 

        j = i - 1 

        while j >= 0 and array[j] > key: 

            array[j + 1] = array[j] 

            j -= 1 

        array[j + 1] = key 

``` 

  

**Ejemplo:** 

  

```python 

array = [5, 2, 9, 1, 5, 6] 

insertion_sort(array) 

print(array) 

``` 

  

Vector original: `[5, 2, 9, 1, 5, 6]` 

  

Después de ordenar: `[1, 2, 5, 5, 6, 9]` 

  

### 2.2. Ordenamiento por Selección 

  

**Definición:** El ordenamiento por selección encuentra el elemento mínimo (o máximo) y lo coloca en la primera posición, luego repite el proceso para el resto del vector. 

  

**Sintaxis/Estructura:** 

  

```python 

def selection_sort(array): 

    for i in range(len(array)): 

        min_index = i 

        for j in range(i + 1, len(array)): 

            if array[j] < array[min_index]: 

                min_index = j 

        array[i], array[min_index] = array[min_index], array[i] 

``` 

  

**Ejemplo:** 

  

```python 

array = [64, 25, 12, 22, 11] 

selection_sort(array) 

print(array) 

``` 

  

Vector original: `[64, 25, 12, 22, 11]` 

  

Después de ordenar: `[11, 12, 22, 25, 64]` 

  

### 2.3. Ordenamiento por Burbujeo 

  

**Definición:** El ordenamiento por burbujeo compara pares de elementos adyacentes y los intercambia si están en el orden incorrecto. 

  

**Sintaxis/Estructura:** 

  

```python 

def bubble_sort(array): 

    n = len(array) 

    for i in range(n): 

        for j in range(0, n-i-1): 

            if array[j] > array[j + 1]: 

                array[j], array[j + 1] = array[j + 1], array[j] 

``` 

  

**Ejemplo:** 

  

```python 

array = [64, 34, 25, 12, 22, 11, 90] 

bubble_sort(array) 

print(array) 

``` 

  

Vector original: `[64, 34, 25, 12, 22, 11, 90]` 

  

Después de ordenar: `[11, 12, 22, 25, 34, 64, 90]` 

  

## 3. Métodos de Ordenamiento no Elementales 

  

### 3.1. Ordenamiento por Shell 

  

**Definición:** El ordenamiento por Shell es una generalización del ordenamiento por inserción que permite intercambiar elementos distantes. 

  

**Sintaxis/Estructura:** 

  

```python 

def shell_sort(array): 

    n = len(array) 

    gap = n // 2 

    while gap > 0: 

        for i in range(gap, n): 

            temp = array[i] 

            j = i 

            while j >= gap and array[j - gap] > temp: 

                array[j] = array[j - gap] 

                j -= gap 

            array[j] = temp 

        gap //= 2 

``` 

  

**Ejemplo:** 

  

```python 

array = [5, 2, 9, 1, 5, 6] 

shell_sort(array) 

print(array) 

``` 

  

Vector original: `[5, 2, 9, 1, 5, 6]` 

  

Después de ordenar: `[1, 2, 5, 5, 6, 9]` 

  

### 3.2. Quick Sort 

  

**Definición:** Quick Sort utiliza la técnica de "divide y vencerás" seleccionando un pivote y particionando el vector en dos subvectores. 

  

**Sintaxis/Estructura:** 

  

```python 

def quick_sort(array): 

    if len(array) <= 1: 

        return array 

    pivot = array[len(array) // 2] 

    left = [x for x in array if x < pivot] 

    middle = [x for x in array if x == pivot] 

    right = [x for x in array if x > pivot] 

    return quick_sort(left) + middle + quick_sort(right) 

``` 

  

**Ejemplo:** 

  

```python 

array = [3, 6, 8, 10, 1, 2, 1] 

array = quick_sort(array) 

print(array) 

``` 

  

Vector original: `[3, 6, 8, 10, 1, 2, 1]` 

  

Después de ordenar: `[1, 1, 2, 3, 6, 8, 10]` 

  

### 3.3. Ordenamiento por Fusión 

  

**Definición:** El ordenamiento por fusión divide el vector en mitades, las ordena recursivamente y luego fusiona las mitades ordenadas. 

  

**Sintaxis/Estructura:** 

  

```python 

def merge_sort(array): 

    if len(array) > 1: 

        mid = len(array) // 2 

        left_half = array[:mid] 

        right_half = array[mid:] 

        merge_sort(left_half) 

        merge_sort(right_half) 

        i = j = k = 0 

        while i < len(left_half) and j < len(right_half): 

            if left_half[i] < right_half[j]: 

                array[k] = left_half[i] 

                i += 1 

            else: 

                array[k] = right_half[j] 

                j += 1 

            k += 1 

        while i < len(left_half): 

            array[k] = left_half[i] 

            i += 1 

            k += 1 

        while j < len(right_half): 

            array[k] = right_half[j] 

            j += 1 

            k += 1 

``` 

  

**Ejemplo:** 

  

```python 

array = [38, 27, 43, 3, 9, 82, 10] 

merge_sort(array) 

print(array) 

``` 

  

Vector original: `[38, 27, 43, 3, 9, 82, 10]` 

  

Después de ordenar: `[3, 9, 10, 27, 38, 43, 82]` 

  

--- 

  

Puedes copiar este contenido a un archivo de texto y guardarlo en formato PDF usando herramientas como Google Docs, Microsoft Word, o cualquier editor de texto que permita exportar a PDF. Si necesitas ayuda con eso, avísame. 
