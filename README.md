# 🎯 MATLAB Motion Analysis - Prosthesis & Flexion Glove Comparator

## 🔄 **Repositorio: MATLAB-Motion-Analysis**

**Descripción del Repositorio:**
*"Sistema avanzado de análisis de coordinación motriz para sistemas de rehabilitación y control protésico. Este repositorio implementa tres algoritmos complementarios que evalúan sincronización, dirección y distancia entre señales de motor de prótesis y guante de flexión, generando métricas cuantitativas para investigación biomecánica."*

---

## 📋 **Resumen del Proyecto - Análisis de Movimiento Multidimensional**

### 🎯 **Propósito General**
Una suite de análisis que evalúa la coordinación entre dispositivos de asistencia motriz mediante tres enfoques complementarios: dirección del movimiento, distancia recorrida y análisis combinado, proporcionando una evaluación integral de la sincronización motriz.

## 🏗️ **Arquitectura del Sistema**

### **📊 Tres Módulos de Análisis**

```
1. ANÁLISIS DE DIRECCIÓN → Pendientes y tendencias
2. ANÁLISIS COMBINADO → Dirección + Distancia  
3. ANÁLISIS DE DISTANCIA → Diferenciales absolutos
```

## 🔢 **Módulo 1: Análisis de Dirección Pura**

### **🎯 Evaluación de Sincronización en Tendencias**

#### **Código 1 - Sistema de Scoring Simple**
```matlab
% Lógica de recompensa básica
if pendientes_opuestas
    recompensa = -1;
elseif pendientes_sincronizadas  
    recompensa = +1;
end
```

#### **Caso de Estudio 1**
- **Matriz1**: [1600, 1400, 1800, 1200, 1432]
- **Matriz2**: [900, 700, 1100, 500, 732]
- **Enfoque**: Solo dirección, sin considerar magnitud

#### **Caso de Estudio 2**  
- **Matriz1**: [1100, 1400, 1800, 1200, 1200]
- **Matriz2**: [900, 700, 1100, 500, 500]
- **Scoring mejorado**: -3, -2, +3 para mayor granularidad

## 🌀 **Módulo 2: Análisis Combinado Dirección-Distancia**

### **⚖️ Sistema Híbrido de Evaluación**

#### **Estructura de Datos**
```matlab
prosthesis_distance = [700, 1100, 500, 732];
glove_distance = [1400, 1800, 1200, 1432];
prosthesis_direction = [1200, 700, 1100, 500, 732];
glove_direction = [1900, 1400, 1800, 1200, 1432];
```

#### **📐 Cálculo de Diferencial de Distancia**
```matlab
for i = 1:4
    diferencia = abs(prosthesis_distance(i) - glove_distance(i));
    sumatoria_diferencias = sumatoria_diferencias + diferencia;
end
```

### **🎯 Sistema de Scoring Adaptativo por Rangos**

#### **Escala de Recompensa Inteligente**
```matlab
% Basado en sumatoria_diferencias
if sumatoria_diferencias == 0
    recompensa = +6;        % Perfecta sincronización
elseif sumatoria_diferencias <= 100
    recompensa = +4;        % Buena sincronización  
elseif sumatoria_diferencias <= 200
    recompensa = +2;        % Sincronización aceptable
else
    recompensa = -2;        % Desincronización
```

#### **Penalizaciones por Dirección Opuesta**
- **Pendientes completamente opuestas**: -6 puntos
- **Una activa, otra inactiva**: -4 puntos

## 📊 **Módulo 3: Análisis de Distancia Pura**

### **📏 Evaluación de Magnitudes Absolutas**

#### **Procesamiento de Datos de Distancia**
```matlab
prosthesis_distance = [700, 1100, 500, 732];
glove_distance = [1400, 1800, 1200, 1432];
```

#### **🖥️ Visualización Especializada**
```matlab
f = figure(1);
ax = subplot(1, 1, 1, "Parent", f);
plot(ax, prosthesis_distance(:, 1));
plot(ax, glove_distance(:, 1));
```

### **📈 Cálculo de Diferencial Acumulado**
```matlab
sumatoria_diferencias = 0;
for i = 1:4
    diferencia = abs(prosthesis_distance(i) - glove_distance(i));
    sumatoria_diferencias = sumatoria_diferencias + diferencia;
end
```

## 🎯 **Sistemas de Scoring Comparativos**

### **📋 Resumen de Estrategias de Recompensa**

| Módulo | Recompensa Máxima | Penalización Máxima | Factores Considerados |
|--------|-------------------|---------------------|----------------------|
| **Dirección** | +1 | -1 | Solo tendencias |
| **Dirección Mejorado** | +3 | -3 | Tendencia + intensidad |
| **Combinado** | +6 | -6 | Tendencia + distancia |
| **Distancia** | N/A | Sumatoria negativa | Solo magnitudes |

### **🔍 Evolución de la Complejidad**
1. **Código 1**: Evaluación binaria simple
2. **Código 1 (2do caso)**: Escala de 3 niveles  
3. **Código 2**: Sistema híbrido adaptativo
4. **Código 3**: Análisis puro de magnitudes

## 💡 **Aplicaciones Específicas por Módulo**

### **🏥 Dirección Pura (Código 1)**
- **Uso**: Evaluación rápida de coordinación básica
- **Ventaja**: Simpleza computacional
- **Caso ideal**: Screening inicial de pacientes

### **🔬 Combinado (Código 2)**
- **Uso**: Investigación científica detallada
- **Ventaja**: Análisis multidimensional
- **Caso ideal**: Estudios de validación de dispositivos

### **📏 Distancia Pura (Código 3)**
- **Uso**: Análisis de eficiencia energética
- **Ventaja**: Enfoque en magnitud del movimiento
- **Caso ideal**: Optimización de consumo en prótesis

## 🛠️ **Características Técnicas**

### **📈 Visualización Unificada**
```matlab
% Estilo consistente en todos los módulos
plot(indices, data, '-o', 'LineWidth', 2, 'MarkerSize', 8);
xlabel('Índices'); ylabel('Valor'); grid on;
legend('Prosthesis motor', 'Flexion glove');
```

### **📊 Salidas de Diagnóstico**
- **Pendientes calculadas**: Tendencias por intervalo
- **Diferencias brutas**: Análisis cuantitativo directo
- **Diferencias modificadas**: Scoring aplicado
- **Recompensa final**: Métrica resumen

## 🎯 **Flujos de Trabajo Recomendados**

### **🔧 Para Desarrollo de Dispositivos**
```
Pruebas Iniciales → Código 1 (Dirección) 
Optimización → Código 3 (Distancia)
Validación Final → Código 2 (Combinado)
```

### **👨‍⚕️ Para Evaluación Clínica**
```
Screening → Código 1 (Rápido)
Análisis Profundo → Código 2 (Completo)
Seguimiento → Código 3 (Magnitudes)
```

## 🌟 **Valor de Investigación**

### **📚 Para Publicaciones Científicas**
- **Métricas cuantitativas**: Datos objetivos para papers
- **Análisis comparativo**: Entre diferentes configuraciones
- **Validación estadística**: Múltiples enfoques de medición
- **Visualización profesional**: Gráficos listos para publicar

### **🎓 Para Educación**
- **Ejemplos prácticos**: Datos realistas incluidos
- **Múltiples enfoques**: Diferentes estrategias de análisis
- **Código documentado**: Fácil de entender y modificar
- **Escalable**: Base para proyectos estudiantiles

## 🚀 **Cómo Ejecutar**

```matlab
% Ejecutar módulo específico
run('direction_analysis.m');    % Código 1
run('combined_analysis.m');     % Código 2  
run('distance_analysis.m');     % Código 3
```

### **📋 Prerrequisitos**
- **MATLAB R2020a** o superior
- **Toolboxes**: Solo funciones base necesarias
- **Hardware**: Cualquier computadora con MATLAB

---
