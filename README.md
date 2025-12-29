# 🏗️ Patrones Creacionales en TypeScript

> *"No preguntes por el objeto, deja que venga a ti"* - Principio de Inversión de Dependencias

## 📋 ¿Qué son los Patrones Creacionales?

Los **patrones creacionales** abstraen el proceso de creación de objetos, haciendo que el sistema sea independiente de cómo sus objetos son creados, compuestos y representados.

## 🎯 Patrones Implementados

### 1. **Factory Method** (`src/factory-method/`)
**Propósito:** Definir una interfaz para crear un objeto, pero dejar que las subclases decidan qué clase instanciar.

```typescript
// Ejemplo: Sistema de notificaciones
interface Notificador {
  enviar(mensaje: string): void;
}

class EmailNotificador implements Notificador {
  enviar(mensaje: string): void {
    console.log(`Enviando email: ${mensaje}`);
  }
}

abstract class CreadorNotificacion {
  public abstract factoryMethod(): Notificador;
  
  public enviarNotificacion(mensaje: string): void {
    const notificador = this.factoryMethod();
    notificador.enviar(mensaje);
  }
}

```