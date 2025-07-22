# DataLoader

El `DataLoader` en PyTorch es una herramienta fundamental para cargar y procesar datos de manera eficiente durante el entrenamiento de modelos de aprendizaje profundo. Te lo explico en detalle:

## ¿Qué es DataLoader?

`DataLoader` es una clase en PyTorch que:
- Proporciona un iterable sobre un conjunto de datos
- Permite cargar datos en lotes (batches)
- Soporta la carga paralela de datos usando múltiples workers
- Ofrece funcionalidades como mezcla (shuffling) de datos

## Componentes principales

1. **Dataset**: Primero necesitas un objeto Dataset que:
   - Herede de `torch.utils.data.Dataset`
   - Implemente `__len__()` (devuelve tamaño del dataset)
   - Implemente `__getitem__()` (devuelve una muestra dado un índice)

2. **DataLoader**: Envuelve tu Dataset y proporciona:
   - Iteración por lotes
   - Mezcla de datos
   - Carga paralela

## Ejemplo básico

```python
import torch
from torch.utils.data import Dataset, DataLoader

# 1. Crear un Dataset personalizado
class MiDataset(Dataset):
    def __init__(self, datos):
        self.datos = datos
    
    def __len__(self):
        return len(self.datos)
    
    def __getitem__(self, idx):
        return self.datos[idx]

# Datos de ejemplo
datos = torch.randn(100, 3, 32, 32)  # 100 imágenes de 3x32x32

# 2. Crear el Dataset
dataset = MiDataset(datos)

# 3. Crear el DataLoader
dataloader = DataLoader(
    dataset,
    batch_size=16,     # Tamaño del lote
    shuffle=True,      # Mezclar los datos
    num_workers=2      # Número de subprocesos para carga de datos
)

# Uso en un ciclo de entrenamiento
for batch in dataloader:
    # batch contiene 16 muestras
    print(batch.shape)  # torch.Size([16, 3, 32, 32])
```

## Parámetros importantes

- `batch_size`: Número de muestras por lote
- `shuffle`: Si mezclar los datos en cada época (normalmente True para entrenamiento)
- `num_workers`: Número de subprocesos para cargar datos (0=solo proceso principal)
- `drop_last`: Si descartar el último lote incompleto
- `pin_memory`: Acelera la transferencia a GPU (útil cuando usas CUDA)

## Ventajas de usar DataLoader

1. **Eficiencia**: Carga datos en paralelo mientras el modelo está entrenando
2. **Flexibilidad**: Fácil de usar con datasets personalizados
3. **Funcionalidades**: Mezcla automática, batching, etc.
4. **Integración**: Funciona perfectamente con los bucles de entrenamiento de PyTorch

## Casos de uso comunes

- Entrenamiento de redes neuronales
- Validación y prueba de modelos
- Procesamiento de grandes conjuntos de datos que no caben en memoria

¿Te gustaría que profundice en algún aspecto específico del DataLoader?