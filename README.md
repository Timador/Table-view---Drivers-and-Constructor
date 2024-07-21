# DriversResult-

        package demo_jdbc.respositories;
        
        import javafx.beans.property.SimpleIntegerProperty;
        import javafx.beans.property.SimpleStringProperty;
        
        public class DriverResult {
            private final SimpleStringProperty driverName;
            private final SimpleIntegerProperty wins;
            private final SimpleIntegerProperty totalPoints;
            private final SimpleIntegerProperty rank;
        
            public DriverResult(String driverName, int wins, int totalPoints, int rank) {
                this.driverName = new SimpleStringProperty(driverName);
                this.wins = new SimpleIntegerProperty(wins);
                this.totalPoints = new SimpleIntegerProperty(totalPoints);
        this.rank = new SimpleIntegerProperty(rank);
            }
        
            public String getDriverName() {
                return driverName.get();
            }
        
            public SimpleStringProperty driverNameProperty() {
                return driverName;
            }
        
            public int getWins() {
                return wins.get();
            }
        
            public SimpleIntegerProperty winsProperty() {
                return wins;
            }
        
            public int getTotalPoints() {
                return totalPoints.get();
            }
        
            public SimpleIntegerProperty totalPointsProperty() {
                return totalPoints;
            }
        
            public int getRank() {
                return rank.get();
            }
        
            public SimpleIntegerProperty rankProperty() {
                return rank;
            }
        }
        
# Drivers-

        package demo_jdbc.models;
        
        public class Driver {
            private int driverId;
            private String driverRef;
            private int number;
            private String code;
            private String forename;
            private String surname;
            private String dob;
            private String nationality;
            private String url;
        
            public Driver(int driverId, String driverRef, int number, String code, String forename, String surname, String dob,
                    String nationality, String url) {
                this.driverId = driverId;
                this.driverRef = driverRef;
                this.number = number;
                this.code = code;
                this.forename = forename;
                this.surname = surname;
                this.dob = dob;
                this.nationality = nationality;
                this.url = url;
            }
        
            // Getters and Setters
            public int getDriverId() {
                return driverId;
            }
        
            public void setDriverId(int driverId) {
                this.driverId = driverId;
            }
        
            public String getDriverRef() {
                return driverRef;
            }
        
            public void setDriverRef(String driverRef) {
                this.driverRef = driverRef;
            }
        
            public int getNumber() {
                return number;
            }
        
            public void setNumber(int number) {
                this.number = number;
            }
        
            public String getCode() {
                return code;
            }
        
            public void setCode(String code) {
                this.code = code;
            }
        
            public String getForename() {
                return forename;
            }
        
            public void setForename(String forename) {
                this.forename = forename;
            }
        
            public String getSurname() {
                return surname;
            }
        
            public void setSurname(String surname) {
                this.surname = surname;
            }
        
            public String getDob() {
                return dob;
            }
        
            public void setDob(String dob) {
                this.dob = dob;
            }
        
            public String getNationality() {
                return nationality;
            }
        
            public void setNationality(String nationality) {
                this.nationality = nationality;
            }
        
            public String getUrl() {
                return url;
            }
        
            public void setUrl(String url) {
                this.url = url;
            }
        }


# ConstructorResult-

        package demo_jdbc.respositories;
        
        public class ConstructorResult {
        
            private String constructorName;
            private int wins;
            private int totalPoints;
            private int rank;
        
            public ConstructorResult(String constructorName, int wins, int totalPoints, int rank) {
                this.constructorName = constructorName;
                this.wins = wins;
                this.totalPoints = totalPoints;
                this.rank = rank;
            }
        
            public String getConstructorName() {
                return constructorName;
            }
        
            public void setConstructorName(String constructorName) {
                this.constructorName = constructorName;
            }
        
            public int getWins() {
                return wins;
            }
        
            public void setWins(int wins) {
                this.wins = wins;
            }
        
            public int getTotalPoints() {
                return totalPoints;
            }
        
            public void setTotalPoints(int totalPoints) {
                this.totalPoints = totalPoints;
            }
        
            public int getRank() {
                return rank;
            }
        
            public void setRank(int rank) {
                this.rank = rank;
            }
        }
        

# Constructor-
        
        package demo_jdbc.models;
        
        import javafx.beans.property.SimpleIntegerProperty;
        import javafx.beans.property.SimpleStringProperty;
        
        public class Constructor {
            private final SimpleIntegerProperty constructorId;
            private final SimpleStringProperty name;
        
            public Constructor(int constructorId, String name) {
                this.constructorId = new SimpleIntegerProperty(constructorId);
                this.name = new SimpleStringProperty(name);
            }
        
            public int getConstructorId() {
                return constructorId.get();
            }
        
            public SimpleIntegerProperty constructorIdProperty() {
                return constructorId;
            }
        
            public String getName() {
                return name.get();
            }
        
            public SimpleStringProperty nameProperty() {
                return name;
            }
        }
        
        
        
        
# Main-
        
        package demo_jdbc;
        
        import java.sql.Connection;
        import java.sql.DriverManager;
        import java.sql.ResultSet;
        import java.sql.Statement;
        
        import demo_jdbc.respositories.ConstructorResult;
        import demo_jdbc.respositories.DriverResult;
        import javafx.application.Application;
        import javafx.collections.FXCollections;
        import javafx.collections.ObservableList;
        import javafx.geometry.Pos;
        import javafx.scene.Scene;
        import javafx.scene.control.ComboBox;
        import javafx.scene.control.TableColumn;
        import javafx.scene.control.TableView;
        import javafx.scene.control.cell.PropertyValueFactory;
        import javafx.scene.layout.BorderPane;
        import javafx.scene.layout.VBox;
        import javafx.stage.Stage;
        
        public class Main extends Application {
        
            private ObservableList<DriverResult> driverResults = FXCollections.observableArrayList();
            private ObservableList<ConstructorResult> constructorResults = FXCollections.observableArrayList();
            private TableView<DriverResult> driverTableView = new TableView<>();
            private TableView<ConstructorResult> constructorTableView = new TableView<>();
            private ComboBox<String> typeComboBox = new ComboBox<>();
            private ComboBox<Integer> yearComboBox = new ComboBox<>();
        
            @Override
            public void start(Stage primaryStage) throws Exception {
                BorderPane borderPane = new BorderPane();
                
                // Configurar ComboBox para elegir tipo de resultados
                typeComboBox.getItems().addAll("Pilotos", "Constructores");
                typeComboBox.setValue("Pilotos"); // Valor por defecto
                typeComboBox.setOnAction(event -> {
                    String selectedType = typeComboBox.getValue();
                    if (selectedType.equals("Pilotos")) {
                        loadDriverResults(yearComboBox.getValue());
                        borderPane.setCenter(driverTableView);
                    } else if (selectedType.equals("Constructores")) {
                        loadConstructorResults(yearComboBox.getValue());
                        borderPane.setCenter(constructorTableView);
                    }
                });
                typeComboBox.setStyle("-fx-alignment: CENTER;");
        
                // Cargar los años disponibles desde la base de datos
                loadYearsFromDatabase();
        
                // Configurar ComboBox de años
                yearComboBox.setOnAction(event -> {
                    String selectedType = typeComboBox.getValue();
                    if (selectedType.equals("Pilotos")) {
                        loadDriverResults(yearComboBox.getValue());
                        borderPane.setCenter(driverTableView);
                    } else if (selectedType.equals("Constructores")) {
                        loadConstructorResults(yearComboBox.getValue());
                        borderPane.setCenter(constructorTableView);
                    }
                });
                yearComboBox.setStyle("-fx-alignment: CENTER;");
        
                // Crear columnas de TableView para pilotos
                TableColumn<DriverResult, String> driverNameColumn = new TableColumn<>("Nombre del Piloto");
                driverNameColumn.setCellValueFactory(new PropertyValueFactory<>("driverName"));
        
                TableColumn<DriverResult, Integer> driverWinsColumn = new TableColumn<>("Victorias");
                driverWinsColumn.setCellValueFactory(new PropertyValueFactory<>("wins"));
        
                TableColumn<DriverResult, Integer> driverPointsColumn = new TableColumn<>("Puntos Totales");
                driverPointsColumn.setCellValueFactory(new PropertyValueFactory<>("totalPoints"));
        
                TableColumn<DriverResult, Integer> driverRankColumn = new TableColumn<>("Ranking");
                driverRankColumn.setCellValueFactory(new PropertyValueFactory<>("rank"));
        
                driverTableView.getColumns().addAll(driverNameColumn, driverWinsColumn, driverPointsColumn, driverRankColumn);
                driverTableView.setItems(driverResults);
                driverTableView.setColumnResizePolicy(TableView.CONSTRAINED_RESIZE_POLICY);
        
                // Crear columnas de TableView para constructores
                TableColumn<ConstructorResult, String> constructorNameColumn = new TableColumn<>("Nombre del Constructor");
                constructorNameColumn.setCellValueFactory(new PropertyValueFactory<>("constructorName"));
        
                TableColumn<ConstructorResult, Integer> constructorWinsColumn = new TableColumn<>("Victorias");
                constructorWinsColumn.setCellValueFactory(new PropertyValueFactory<>("wins"));
        
                TableColumn<ConstructorResult, Integer> constructorPointsColumn = new TableColumn<>("Puntos Totales");
                constructorPointsColumn.setCellValueFactory(new PropertyValueFactory<>("totalPoints"));
        
                TableColumn<ConstructorResult, Integer> constructorRankColumn = new TableColumn<>("Ranking");
                constructorRankColumn.setCellValueFactory(new PropertyValueFactory<>("rank"));
        
                constructorTableView.getColumns().addAll(constructorNameColumn, constructorWinsColumn, constructorPointsColumn, constructorRankColumn);
                constructorTableView.setItems(constructorResults);
                constructorTableView.setColumnResizePolicy(TableView.CONSTRAINED_RESIZE_POLICY);
        
                // Crear layout y agregar componentes
                VBox vbox = new VBox();
                vbox.setAlignment(Pos.CENTER);
                vbox.getChildren().addAll(typeComboBox, yearComboBox);
        
                borderPane.setTop(vbox);
                borderPane.setCenter(driverTableView); // Mostrar inicialmente resultados de pilotos
        
                // Crear la escena y mostrarla
                Scene scene = new Scene(borderPane, 800, 600);
                primaryStage.setTitle("Resultados de Pilotos y Constructores");
                primaryStage.setScene(scene);
                primaryStage.show();
            }
        
            private void loadYearsFromDatabase() {
                String url = "jdbc:postgresql://localhost:2003/formula1";
                String user = "postgres";
                String password = "postgresql.2003";
                String query = "SELECT DISTINCT year FROM races ORDER BY year";
        
                try {
                    Class.forName("org.postgresql.Driver");
                    Connection conn = DriverManager.getConnection(url, user, password);
                    Statement stmt = conn.createStatement();
                    ResultSet rs = stmt.executeQuery(query);
        
                    while (rs.next()) {
                        int year = rs.getInt("year");
                        yearComboBox.getItems().add(year);
                    }
        
                    rs.close();
                    stmt.close();
                    conn.close();
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
        
            private void loadDriverResults(int year) {
                driverResults.clear();
                String url = "jdbc:postgresql://localhost:2003/formula1";
                String user = "postgres";
                String password = "postgresql.2003";
                String query = "SELECT * FROM ("
                        + " SELECT r.year, d.forename || ' ' || d.surname AS driver_name, "
                        + " COUNT(CASE WHEN res.position = 1 THEN 1 END) AS wins, "
                        + " SUM(res.points) AS total_points, "
                        + " ROW_NUMBER() OVER (PARTITION BY r.year ORDER BY SUM(res.points) DESC, COUNT(CASE WHEN res.position = 1 THEN 1 END) DESC) AS rank "
                        + " FROM results res "
                        + " JOIN races r ON res.raceid = r.raceid "
                        + " JOIN drivers d ON res.driverid = d.driverid "
                        + " WHERE r.year = " + year + " "
                        + " GROUP BY r.year, d.driverid, d.forename, d.surname"
                        + ") AS ranked_results "
                        + "ORDER BY year, rank;";
        
                try {
                    Class.forName("org.postgresql.Driver");
                    Connection conn = DriverManager.getConnection(url, user, password);
                    Statement stmt = conn.createStatement();
                    ResultSet rs = stmt.executeQuery(query);
        
                    while (rs.next()) {
                        String driverName = rs.getString("driver_name");
                        int wins = rs.getInt("wins");
                        int totalPoints = rs.getInt("total_points");
                        int rank = rs.getInt("rank");
        
                        DriverResult result = new DriverResult(driverName, wins, totalPoints, rank);
                        driverResults.add(result);
                    }
        
                    rs.close();
                    stmt.close();
                    conn.close();
                } catch (Exception e) {
                    e.printStackTrace();
                }
        
                // Actualizar TableView
                driverTableView.setItems(driverResults);
            }
        
            private void loadConstructorResults(int year) {
                constructorResults.clear();
                String url = "jdbc:postgresql://localhost:2003/formula1";
                String user = "postgres";
                String password = "postgresql.2003";
                String query = "SELECT * FROM ("
                        + " SELECT r.year, c.name AS constructor_name, "
                        + " COUNT(CASE WHEN res.position = 1 THEN 1 END) AS wins, "
                        + " SUM(res.points) AS total_points, "
                        + " ROW_NUMBER() OVER (PARTITION BY r.year ORDER BY SUM(res.points) DESC, COUNT(CASE WHEN res.position = 1 THEN 1 END) DESC) AS rank "
                        + " FROM results res "
                        + " JOIN races r ON res.raceid = r.raceid "
                        + " JOIN constructor c ON res.constructorid = c.constructorid "
                        + " WHERE r.year = " + year + " "
                        + " GROUP BY r.year, c.constructorid, c.name"
                        + ") AS ranked_results "
                        + "ORDER BY year, rank;";
        
                try {
                    Class.forName("org.postgresql.Driver");
                    Connection conn = DriverManager.getConnection(url, user, password);
                    Statement stmt = conn.createStatement();
                    ResultSet rs = stmt.executeQuery(query);
        
                    while (rs.next()) {
                        String constructorName = rs.getString("constructor_name");
                        int wins = rs.getInt("wins");
                        int totalPoints = rs.getInt("total_points");
                        int rank = rs.getInt("rank");
        
                        ConstructorResult result = new ConstructorResult(constructorName, wins, totalPoints, rank);
                        constructorResults.add(result);
                    }
        
                    rs.close();
                    stmt.close();
                    conn.close();
                } catch (Exception e) {
                    e.printStackTrace();
                }
        
                // Actualizar TableView
                constructorTableView.setItems(constructorResults);
            }
        
            public static void main(String[] args) {
                launch(args);
            }
        }


![image](https://github.com/user-attachments/assets/8bebbf34-e81a-4099-bb5b-5f989fae8f45)

![Imagen de WhatsApp 2024-07-15 a las 11 39 39_9c813e28](https://github.com/user-attachments/assets/0e6c14b3-7884-4c52-8b18-3711a45db3c7)

