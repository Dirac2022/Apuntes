
```
#include <iostream>

// Mitchel Soto Cuya
// 20222096I
// Tarea AD Algoritmos

using namespace std;

int binarysearch(int array[], int target, int init, int fin) {

    if (init <= fin) {
        int middle = (init + fin) / 2;  

        if (array[middle] == target) {
            return middle;
        }

        else if (array[middle] < target) {
                return binarysearch(array, target, middle + 1, fin);
            }

        else {
            return binarysearch(array, target, init, middle - 1);
        }
    }

    else {
        return -1;
    }  
}

  

int main() {

    int arreglo [] = {2,4,6,9,10,45,220};
    int tam = sizeof(arreglo) / sizeof(arreglo[0]);
    int pos = binarysearch(arreglo, 45, 0, tam -1);

    if (pos == -1) {
        cout << "El valor no se encuentra en el arreglo" << endl;
    }

    else {
        cout << "El valor se encuentra en la posicion: "  << pos << endl;
    }
}
```