# Tablas-de-Multiplicar

#Morales Henry

package com.mycompany.tablas_de_multiplicar;

import java.util.*;
import java.util.concurrent.*;
import java.util.stream.*;

public class Tablas_de_Multiplicar {

    // *** Programacion OrientadA a Objetos ***
    // Clase para representar una tabla de multiplicar
    static class Tabla {

        private int num;

        // Constructor: inicializa la tabla con el número ingresado
        public Tabla(int num) {
            this.num = num;
        }

        // Getter para obtener el número de la tabla
        public int getNumero() {
            return num;
        }

        // Setter para cambiar el número de la tabla
        public void setNumero(int number) {
            this.num = number;
        }

        // Método para mostrar la tabla de multiplicar
        public void mostrarTabla() {
            System.out.println("Tabla de multiplicar (POO): " + num);
            // donde esta el 12 se puede cambiar el numero, es un ciclo que se repitira hasta el numero que deseas
            for (int i = 1; i <= 12; i++) {
                System.out.println(num + " x " + i + " = " + (num * i));
            }
        }
    }

    // *** Procedural ***
    // Método que muestra la tabla de multiplicar de manera procedural
    public static void mostrarProceduralTabla(int num) {
        System.out.println("Tabla de multiplicar (Procedural): " + num);
        // donde esta el 12 se puede cambiar el numero es un ciclo que se repitira hasta el numero que deseas

        for (int i = 1; i <= 12; i++) {
            System.out.println(num+ " x " + i + " = " + (num* i));
        }
    }

    // *** Funcional ***
    // Método que usa programación funcional para mostrar la tabla
    public static void mostrarFunctionalTabla(int num) {
        System.out.println("Tabla de multiplicar (Funcional): " + num );
        IntStream.rangeClosed(1, 12) // Genera números del 1 al 12
                .forEach(i -> System.out.println(num + " x " + i + " = " + (num* i)));
    }

    // *** Concurrente ***
    // Método que muestra la tabla de multiplicar usando múltiples hilos
    public static void mostrarConcurrentTabla(int num) {
        System.out.println("Tabla de multiplicar (Concurrente): " + num);
        ExecutorService executor = Executors.newFixedThreadPool(4); // Crea un grupo de 4 hilos 
        for (int i = 1; i <= 12; i++) {
            int mul = i; // Necesario para usar en la expresión lambda
            executor.submit(() -> {
                // Cada hilo imprime una multiplicación
                System.out.println(num+ " x " + mul + " = " + (num* mul));
            });
        }
        executor.shutdown(); // Indica que no se enviarán más tareas
        try {
            executor.awaitTermination(1, TimeUnit.SECONDS); // Espera a que todas las tareas finalicen
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in); // Objeto para leer la entrada del usuario

        // Solicita al usuario un número para generar la tabla
        System.out.print("Introduce el numero que deseas saber la tabla de multiplicar: ");
        int number = scanner.nextInt(); // Lee el número ingresado

        // Llama al método procedural para mostrar la tabla
        mostrarProceduralTabla(number);

        // Orientado a Objetos: crea una instancia de la clase Table y llama a su método
        Tabla table = new Tabla(number);
        table.mostrarTabla();

        // Llama al método funcional para mostrar la tabla
        mostrarFunctionalTabla(number);

        // Llama al método concurrente para mostrar la tabla
        mostrarConcurrentTabla(number);

        scanner.close(); // Cierra el objeto Scanner
    }
}
