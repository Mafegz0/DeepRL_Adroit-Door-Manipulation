# Deep Reinforcement Learning – Adroit Door Manipulation (PPO vs SAC)

## Descripción del Proyecto

Este proyecto implementa agentes de Aprendizaje por Refuerzo Profundo (Deep Reinforcement Learning) para resolver una tarea de manipulación robótica en el entorno AdroitHandDoor-v1 utilizando los algoritmos Proximal Policy Optimization (PPO) y Soft Actor-Critic (SAC) mediante la librería Stable-Baselines3.

El objetivo del agente es aprender a controlar una mano robótica con múltiples grados de libertad para interactuar con la manija de una puerta y ejecutar movimientos que permitan abrirla.

## ¿Qué es Adroit Hand Door?

El entorno Adroit Hand Door pertenece al paquete Gymnasium Robotics y simula una mano robótica Shadow Hand con aproximadamente 30 grados de libertad.

El agente debe aprender a:

- Posicionar la mano correctamente frente a la puerta.
- Acercarse a la manija.
- Realizar movimientos de agarre.
- Aplicar acciones coordinadas para abrir la puerta.

Desde la perspectiva del aprendizaje por refuerzo, este entorno presenta desafíos importantes:

- Espacio de acción continuo de alta dimensión  
- Gran número de grados de libertad  
- Dinámica física compleja simulada en MuJoCo  
- Necesidad de coordinación fina entre articulaciones  

Estas características lo convierten en un entorno adecuado para evaluar algoritmos avanzados de control continuo.

## Objetivo del Proyecto

Entrenar agentes capaces de aprender una política que supere el comportamiento aleatorio en el entorno AdroitHandDoor-v1, utilizando diferentes algoritmos de aprendizaje por refuerzo profundo.

El proyecto compara específicamente el desempeño de:

- Proximal Policy Optimization (PPO)  
- Soft Actor-Critic (SAC)  

Analizando:

- estabilidad del aprendizaje  
- eficiencia del entrenamiento  
- capacidad de exploración  
- desempeño final del agente  

## Algoritmos Implementados

### Proximal Policy Optimization (PPO)

PPO es un algoritmo on-policy basado en gradientes de política que optimiza la política del agente mediante una función objetivo con clipping, evitando actualizaciones demasiado grandes que puedan desestabilizar el aprendizaje.

Características principales:

- Actualización estable de la política  
- Uso de Generalized Advantage Estimation (GAE)  
- Optimización por minibatches  
- Entrenamiento directo de actor y crítico  

Aunque PPO es robusto y ampliamente utilizado, en entornos de control continuo de alta dimensionalidad puede requerir mayor cantidad de interacciones con el entorno.

### Soft Actor-Critic (SAC)

SAC es un algoritmo off-policy diseñado para espacios de acción continuos. Utiliza el principio de máxima entropía, lo que fomenta la exploración del agente durante el aprendizaje.

Características principales:

- Replay Buffer para reutilizar experiencias  
- Optimización actor–critic  
- Regularización por entropía  
- Exploración eficiente mediante State Dependent Exploration (SDE)  

Este enfoque permite un aprendizaje más eficiente en entornos complejos como la manipulación robótica.

## Configuración del Entrenamiento

### PPO

- Total timesteps: 120,000 – 286,000  
- Learning rate: 3e-4  
- Batch size: 256  
- Epochs: 10  
- Gamma: 0.99  
- GAE lambda: 0.95  
- Clip range: 0.2  
- Entropy coefficient: 0.01  

### SAC

Configuración optimizada utilizada:

- Total timesteps: 300,000  
- Learning rate: 3e-4  
- Replay buffer: 300,000  
- Batch size: 256  
- Learning starts: 10,000  
- Gamma: 0.99  
- Tau: 0.005  
- Entropy coefficient: auto  
- State Dependent Exploration: True  
- Red neuronal: [256,256]  
- Activación: ReLU  
- Dispositivo: GPU (CUDA)  

## Resultados

Los experimentos muestran diferencias claras entre los algoritmos.

### PPO

- Recompensa promedio aproximada: -31  
- Aprendizaje limitado  
- Mejora leve respecto a política aleatoria  

### SAC (optimizado)

- Recompensa promedio: 1111.60  
- Alta variabilidad entre episodios  
- Episodios con recompensas superiores a 3000  

Esto indica que SAC logra explorar mejor el espacio de acciones y aprender comportamientos más efectivos para manipular la puerta.

## Análisis con TensorBoard

Las gráficas de TensorBoard muestran claramente la diferencia en el comportamiento de aprendizaje entre ambos algoritmos.

Las curvas de PPO permanecen cerca de valores negativos durante el entrenamiento.  
La curva de SAC presenta un aumento significativo en la recompensa promedio a partir de aproximadamente 200k pasos, alcanzando valores superiores a 200 en promedio.

Esto evidencia que SAC logra desarrollar una política más efectiva para este entorno de control continuo.

## Contenido del Repositorio
```
AdroitDoor/
│
├── sac_adroit_door_model_v2.zip
├── video_entrenamiento.mp4
├── video_r2737.mp4
│
├── logs/
│   ├── adroit_sac_3/
│   └── checkpoints/
└── Adroit_Door_PPO_SAC_final.ipynb
```

Los videos incluidos muestran el comportamiento del agente aprendido durante el entrenamiento.

## Hardware Utilizado

- Google Colab  
- GPU NVIDIA (CUDA)  
- Stable-Baselines3  
- Gymnasium Robotics  
- MuJoCo
  
## Conclusión

Los resultados obtenidos muestran que Soft Actor-Critic (SAC) es significativamente más efectivo que PPO para resolver el problema de manipulación robótica en AdroitHandDoor-v1. Mientras PPO presenta mejoras limitadas sobre una política aleatoria, SAC logra aprender políticas más complejas gracias a su enfoque off-policy, el uso de replay buffer y la optimización basada en máxima entropía, lo que facilita una exploración más eficiente del espacio de acciones.

En consecuencia, los experimentos evidencian que algoritmos off-policy como SAC presentan ventajas importantes en entornos de control continuo y alta dimensionalidad como los de manipulación robótica.
