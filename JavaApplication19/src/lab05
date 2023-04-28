import java.io.BufferedWriter;
import java.io.File;
import java.io.FileWriter;
import java.io.IOException;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Conexión a la base de datos
        Connection conn = null;
        Statement stmt = null;
        ResultSet rs = null;
        try {
            Class.forName("com.mysql.jdbc.Driver").newInstance();
            String url = "jdbc:mysql://localhost:3306/nombre_de_la_bd";
            String user = "tu_usuario";
            String password = "tu_contraseña";
            conn = DriverManager.getConnection(url, user, password);
            stmt = conn.createStatement();
        } catch (Exception e) {
            e.printStackTrace();
        }

        // Variables para los filtros
        String ciudad = "";
        int edadMinima = 0;
        int edadMaxima = 100;
        boolean pobrezaMonetaria = false;
        boolean pobrezaMonetariaExtrema = false;

        // Obtener los valores de los filtros
        ArrayList<String> ciudades = new ArrayList<String>();
        ArrayList<Integer> edades = new ArrayList<Integer>();
        try {
            rs = stmt.executeQuery("SELECT DISTINCT ciudad FROM tabla");
            while (rs.next()) {
                ciudades.add(rs.getString("ciudad"));
            }
            rs = stmt.executeQuery("SELECT DISTINCT edad FROM tabla");
            while (rs.next()) {
                edades.add(rs.getInt("edad"));
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }

        // Mostrar los filtros disponibles
        System.out.println("Filtros disponibles:");
        System.out.println("1. Ciudad");
        System.out.println("2. Edad mínima");
        System.out.println("3. Edad máxima");
        System.out.println("4. Pobreza monetaria");
        System.out.println("5. Pobreza monetaria extrema");

        // Pedir al usuario que seleccione los filtros
        System.out.print("Seleccione los filtros que desea aplicar (separados por comas): ");
        String[] opciones = scanner.nextLine().split(",");

        // Aplicar los filtros seleccionados
        for (String opcion : opciones) {
            opcion = opcion.trim();
            switch (opcion) {
                case "1":
                    System.out.println("Ciudades disponibles:");
                    for (String c : ciudades) {
                        System.out.println(c);
                    }
                    System.out.print("Seleccione una ciudad: ");
                    ciudad = scanner.nextLine();
                    break;
                case "2":
                    System.out.print("Ingrese la edad mínima: ");
                    edadMinima = scanner.nextInt();
                    scanner.nextLine();
                    break;
                case "3":
                    System.out.print("Ingrese la edad máxima: ");
                    edadMaxima = scanner.nextInt();
                    scanner.nextLine();
                    break;
                case "4":
                    pobrezaMonetaria = true;
                    break;
                case "5":
                    pobrezaMonetariaExtrema = true;
                    break;
            }
        }

        // Realizar la consulta
        String consulta = "SELECT * FROM tabla WHERE edad >= " + edadMinima + " AND edad <= " + edadMaxima;
        if (!ciudad.equals("")) {
            consulta += " AND ciudad = '" + ciudad + "'";
        }
        if (pobrezaMonetaria) {
            consulta += " AND pobreza
