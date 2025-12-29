
# 🧩 Patrones Estructurales en TypeScript

> *"Componer objetos en estructuras más grandes manteniendo flexibilidad y eficiencia"*

## 📋 ¿Qué son los Patrones Estructurales?

Los **patrones estructurales** se enfocan en cómo las clases y objetos se componen para formar estructuras más grandes, facilitando el diseño de relaciones entre entidades.

## 🎯 Patrones Implementados

### 1. **Adapter** (`src/adapter/`)
**Propósito:** Convertir la interfaz de una clase en otra interfaz que el cliente espera.

```typescript
// Ejemplo: Adaptador de APIs de pago
interface PagoModerno {
  pagar(cantidad: number): boolean;
}

class PagoLegacy {
  procesarPago(monto: number): string {
    return monto > 0 ? "ÉXITO" : "ERROR";
  }
}

class PagoAdapter implements PagoModerno {
  constructor(private legacyPago: PagoLegacy) {}
  
  pagar(cantidad: number): boolean {
    const resultado = this.legacyPago.procesarPago(cantidad);
    return resultado === "ÉXITO";
  }
}
```

## **4. README.md para `behavioral-patterns`:**

