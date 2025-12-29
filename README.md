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
