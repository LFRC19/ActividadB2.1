# ActividadB2.1

Descripción del programa
Este programa es una implementación del patrón de diseño estructural Bridge en C#. Dado que al girar la ruleta el resultado fue "Estructural, Transporte y Comunicación entre Objetos". En este caso, aplique el patrón en el dominio de transporte, donde diferentes medios de transporte (autobuses, trenes) deben comunicarse con una central de control utilizando diferentes tecnologías de comunicación (radio, internet).

Funcionamiento del Programa.
El programa modela un sistema de transporte donde:
Autobuses y trenes pueden enviar mensajes a través de diferentes medios de comunicación (por ejemplo, radio o internet).
El patrón Bridge permite cambiar tanto el medio de transporte como el tipo de comunicación sin alterar el código de las clases existentes, lo que mejora la extensibilidad y mantenibilidad del sistema.


#Codigo
using System;

// Interfaz de comunicación
public interface IComunicacion
{
    void Enviar(string mensaje);
}

// Comunicación por Radio
public class ComunicacionRadio : IComunicacion
{
    public void Enviar(string mensaje)
    {
        Console.WriteLine("Enviando mensaje por Radio: " + mensaje);
    }
}

// Comunicación por Internet
public class ComunicacionInternet : IComunicacion
{
    public void Enviar(string mensaje)
    {
        Console.WriteLine("Enviando mensaje por Internet: " + mensaje);
    }
}

// Abstracción Transporte
public abstract class Transporte
{
    protected IComunicacion comunicacion;

    public Transporte(IComunicacion comunicacion)
    {
        this.comunicacion = comunicacion;
    }

    public abstract void EnviarMensaje(string mensaje);
}

// Implementación concreta de Autobús
public class Autobus : Transporte
{
    public Autobus(IComunicacion comunicacion) : base(comunicacion) { }

    public override void EnviarMensaje(string mensaje)
    {
        Console.WriteLine("Autobús: Preparando para enviar mensaje...");
        comunicacion.Enviar(mensaje);
    }
}

// Implementación concreta de Tren
public class Tren : Transporte
{
    public Tren(IComunicacion comunicacion) : base(comunicacion) { }

    public override void EnviarMensaje(string mensaje)
    {
        Console.WriteLine("Tren: Preparando para enviar mensaje...");
        comunicacion.Enviar(mensaje);
    }
}

class Program
{
    static void Main(string[] args)
    {
        // Instancias de los diferentes medios de comunicación
        IComunicacion radio = new ComunicacionRadio();
        IComunicacion internet = new ComunicacionInternet();

        // Instancias de los diferentes tipos de transporte
        Transporte autobus = new Autobus(radio);
        Transporte tren = new Tren(internet);

        // Enviar mensajes usando diferentes medios de comunicación
        autobus.EnviarMensaje("El autobús está en ruta.");
        tren.EnviarMensaje("El tren ha llegado a la estación.");

        // Evita que la consola se cierre inmediatamente
        Console.ReadLine();
    }
}




Ejemplo de Uso
En este ejemplo, un autobús usa la comunicación por radio y un tren usa la comunicación por internet para enviar mensajes a una central:

Codigo ejemplo:
// Crear instancias de los medios de comunicación
IComunicacion radio = new ComunicacionRadio();
IComunicacion internet = new ComunicacionInternet();

// Crear instancias de los medios de transporte
Transporte autobus = new Autobus(radio);
Transporte tren = new Tren(internet);

// Enviar mensajes usando los diferentes medios de comunicación
autobus.EnviarMensaje("El autobús está en ruta.");
tren.EnviarMensaje("El tren ha llegado a la estación.");

