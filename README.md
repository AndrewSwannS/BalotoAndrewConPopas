/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 * Click nbfs://nbhost/SystemFileSystem/Templates/Classes/Main.java to edit this template
 */
package balotoandrewcConPopas;

/**
 *
 * @author Andrew
 */
import java.util.Set;
import java.util.TreeSet;
import javax.swing.JOptionPane;

public class BalotoAndrewConPopas {

    public static void main(String[] args) {

        String intentar;
        int opcion;

        // Datos login
        String user = "cami";
        String pass = "1234";

        // ===============================
        // LOGIN
        // ===============================
        while (true) {

            String Usuario = JOptionPane.showInputDialog("Ingrese el usuario");
            String Contrasena = JOptionPane.showInputDialog("Ingrese contraseña");

            if (Usuario != null && Contrasena != null
                    && Usuario.equalsIgnoreCase(user) && Contrasena.equals(pass)) {

                JOptionPane.showMessageDialog(null, " Inicio de sesión exitoso");
                break;

            } else {
                JOptionPane.showMessageDialog(null, "Usuario o contraseña incorrectos");
            }
        }

        // ===============================
        // JUEGO
        // ===============================
        do {
            Set<Integer> numeros = new TreeSet<>();
            Set<Integer> ganador = new TreeSet<>();

            // Entrada usuario
            while (numeros.size() < 6) {

                try {
                    String input = JOptionPane.showInputDialog(
                            null,
                            "Elige número " + (numeros.size() + 1) + " (1-45):",
                            " Baloto Andrew",
                            JOptionPane.QUESTION_MESSAGE
                    );
                    if (input == null) {
                        return; // si cancela
                    }
                    int num = Integer.parseInt(input);

                    if (num < 1 || num > 45) {
                        JOptionPane.showMessageDialog(null, " Solo números entre 1 y 45");
                    } else if (!numeros.add(num)) {
                        JOptionPane.showMessageDialog(null, " Número repetido");
                    }

                } catch (Exception e) {
                    JOptionPane.showMessageDialog(null, " Ingresa un número válido");
                }
            }

            // Sorteo aleatorio
            while (ganador.size() < 6) {
                int numGanador = (int) (Math.random() * 45) + 1;
                ganador.add(numGanador);
            }

            // Contar aciertos
            int aciertos = 0;
            for (int n : numeros) {
                if (ganador.contains(n)) {
                    aciertos++;
                }
            }

            // RESULTADO
            String mensaje = " RESULTADOS\n\n"
                    + "TU JUGADA: " + numeros + "\n"
                    + "NÚMEROS GANADORES: " + ganador + "\n"
                    + "ACIERTOS: " + aciertos + "\n\n";

            if (aciertos == 6) {
                mensaje += " ¡Ganaste el premio mayor!";
            } else if (aciertos >= 4) {
                mensaje += " Ganaste premio menor";
            } else {
                mensaje += " ";
            }

            JOptionPane.showMessageDialog(null, mensaje);

            // Preguntar si desea continuar
            opcion = JOptionPane.showConfirmDialog(null, "¿Quieres jugar otra vez?");

            if (opcion == JOptionPane.YES_OPTION) {
                intentar = "s";
            } else {
                intentar = "n";
            }

        } while (intentar.equalsIgnoreCase("s"));

        JOptionPane.showMessageDialog(null, "Gracias por jugar ");
    }
}
