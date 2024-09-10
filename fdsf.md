
# Métodos de Ordenamiento en C++ (sin usar bibliotecas estándar)

## 1. Ordenamiento por Inserción

**Definición:** El algoritmo de ordenamiento por inserción construye el arreglo ordenado uno a uno, colocando cada elemento en su posición correcta.

**Sintaxis/Estructura:**
- Iterar desde el segundo elemento hasta el último.
- Tomar el elemento actual y compararlo con los elementos anteriores.
- Desplazar los elementos mayores a la derecha para insertar el elemento en la posición correcta.

**Código:**

```cpp
#include <iostream>

using namespace std;

void insertionSort(int arr[], int n) {
    for (int i = 1; i < n; ++i) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            --j;
        }
        arr[j + 1] = key;
    }
}

int main() {
    int arr[] = {5, 2, 9, 1, 5, 6};
    int n = sizeof(arr) / sizeof(arr[0]);
    insertionSort(arr, n);
    for (int i = 0; i < n; ++i) cout << arr[i] << " ";
    return 0;
}
```

## 2. Ordenamiento por Selección

**Definición:** El algoritmo de ordenamiento por selección encuentra el elemento mínimo (o máximo) y lo coloca en la primera posición, luego repite el proceso para el resto del arreglo.

**Sintaxis/Estructura:**
- Iterar sobre todo el arreglo y encontrar el índice del elemento mínimo.
- Intercambiar el elemento mínimo encontrado con el primer elemento no ordenado.
- Repetir para el resto del arreglo.

**Código:**

```cpp
#include <iostream>

using namespace std;

void selectionSort(int arr[], int n) {
    for (int i = 0; i < n - 1; ++i) {
        int minIndex = i;
        for (int j = i + 1; j < n; ++j) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        if (minIndex != i) {
            int temp = arr[i];
            arr[i] = arr[minIndex];
            arr[minIndex] = temp;
        }
    }
}

int main() {
    int arr[] = {64, 25, 12, 22, 11};
    int n = sizeof(arr) / sizeof(arr[0]);
    selectionSort(arr, n);
    for (int i = 0; i < n; ++i) cout << arr[i] << " ";
    return 0;
}
```

## 3. Ordenamiento por Burbujeo

**Definición:** El algoritmo de ordenamiento por burbujeo compara pares de elementos adyacentes y los intercambia si están en el orden incorrecto.

**Sintaxis/Estructura:**
- Comparar elementos adyacentes.
- Intercambiar si el elemento de la izquierda es mayor que el de la derecha.
- Repetir hasta que el arreglo esté ordenado.

**Código:**

```cpp
#include <iostream>

using namespace std;

void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n - 1; ++i) {
        for (int j = 0; j < n - i - 1; ++j) {
            if (arr[j] > arr[j + 1]) {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}

int main() {
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    int n = sizeof(arr) / sizeof(arr[0]);
    bubbleSort(arr, n);
    for (int i = 0; i < n; ++i) cout << arr[i] << " ";
    return 0;
}
```

## 4. Ordenamiento por Shell

**Definición:** El algoritmo de ordenamiento por Shell es una generalización del ordenamiento por inserción que permite intercambiar elementos distantes para mejorar la eficiencia.

**Sintaxis/Estructura:**
- Dividir el arreglo en subarreglos usando un intervalo (gap).
- Ordenar los subarreglos usando el algoritmo de inserción.
- Reducir el intervalo y repetir hasta que el intervalo sea 1.

**Código:**

```cpp
#include <iostream>

using namespace std;

void shellSort(int arr[], int n) {
    for (int gap = n / 2; gap > 0; gap /= 2) {
        for (int i = gap; i < n; ++i) {
            int temp = arr[i];
            int j;
            for (j = i; j >= gap && arr[j - gap] > temp; j -= gap) {
                arr[j] = arr[j - gap];
            }
            arr[j] = temp;
        }
    }
}

int main() {
    int arr[] = {5, 2, 9, 1, 5, 6};
    int n = sizeof(arr) / sizeof(arr[0]);
    shellSort(arr, n);
    for (int i = 0; i < n; ++i) cout << arr[i] << " ";
    return 0;
}
```

## 5. Quick Sort

**Definición:** El algoritmo Quick Sort utiliza la técnica de "divide y vencerás" seleccionando un pivote y particionando el arreglo en dos subvectores que se ordenan recursivamente.

**Sintaxis/Estructura:**
- Elegir un pivote.
- Particionar el arreglo en dos partes: menores que el pivote y mayores que el pivote.
- Ordenar recursivamente las dos particiones.

**Código:**

```cpp
#include <iostream>

using namespace std;

int partition(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = low - 1;
    for (int j = low; j < high; ++j) {
        if (arr[j] < pivot) {
            ++i;
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
    }
    int temp = arr[i + 1];
    arr[i + 1] = arr[high];
    arr[high] = temp;
    return i + 1;
}

void quickSort(int arr[], int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

int main() {
    int arr[] = {10, 7, 8, 9, 1, 5};
    int n = sizeof(arr) / sizeof(arr[0]);
    quickSort(arr, 0, n - 1);
    for (int i = 0; i < n; ++i) cout << arr[i] << " ";
    return 0;
}
```

## 6. Ordenamiento por Fusión

**Definición:** El algoritmo de ordenamiento por fusión divide el arreglo en mitades, las ordena recursivamente y luego fusiona las mitades ordenadas.

**Sintaxis/Estructura:**
- Dividir el arreglo en dos mitades.
- Ordenar cada mitad recursivamente.
- Fusionar las dos mitades ordenadas en un arreglo ordenado.

**Código:**

```cpp
#include <iostream>

using namespace std;

void merge(int arr[], int l, int m, int r) {
    int n1 = m - l + 1;
    int n2 = r - m;

    int *L = new int[n1];
    int *R = new int[n2];

    for (int i = 0; i < n1; ++i)
        L[i] = arr[l + i];
    for (int j = 0; j < n2; ++j)
        R[j] = arr[m + 1 + j];

    int i = 0, j = 0, k = l;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k++] = L[i++];
        } else {
            arr[k++] = R[j++];
        }
    }

    while (i < n1) {
        arr[k++] = L[i++];
    }

    while (j < n2) {
        arr[k++] = R[j++];
    }

    delete[] L;
    delete[] R;
}

void mergeSort(int arr[], int l, int r) {
    if (l < r) {
        int m = l + (r - l) / 2;

        mergeSort(arr, l, m);
        mergeSort(arr, m + 1, r);

        merge(arr, l, m, r);
    }
}

int main() {
    int arr[] = {12, 11, 13, 5, 6, 7};
    int n = sizeof(arr) / sizeof(arr[0]);
    mergeSort(arr, 0,

 n - 1);
    for (int i = 0; i < n; ++i) cout << arr[i] << " ";
    return 0;
}
```

