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

## **3. README.md para `structural-patterns`:**

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

# 🤝 Patrones de Comportamiento en TypeScript

> *"Gestionar algoritmos, responsabilidades y comunicación entre objetos"*

## 📋 ¿Qué son los Patrones de Comportamiento?

Los **patrones de comportamiento** se centran en la comunicación efectiva y la asignación de responsabilidades entre objetos, definiendo cómo interactúan y se distribuyen las tareas.

## 🎯 Patrones Implementados

### 1. **Chain of Responsibility** (`src/chain-of-responsibility/`)
**Propósito:** Evitar acoplar el emisor de una petición a su receptor dando a más de un objeto la oportunidad de manejar la petición.

```typescript
// Ejemplo: Middleware pipeline
interface Handler {
  setNext(handler: Handler): Handler;
  handle(request: string): string | null;
}

abstract class Middleware implements Handler {
  private nextHandler: Handler | null = null;
  
  setNext(handler: Handler): Handler {
    this.nextHandler = handler;
    return handler;
  }
  
  handle(request: string): string | null {
    if (this.nextHandler) {
      return this.nextHandler.handle(request);
    }
    return null;
  }
}

class AuthMiddleware extends Middleware {
  handle(request: string): string | null {
    if (request.includes("token=")) {
      console.log("Autenticación exitosa");
      return super.handle(request);
    }
    return "Error de autenticación";
  }
}
```