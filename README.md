import java.util.Scanner;

class Vehicle {
    private static int totalVehicles = 0;
    private static int vehicleCount = 0;
    private String modelName;
    private int speed;

    public Vehicle(String modelName, int speed) {
        this.modelName = modelName;
        this.speed = speed;
        totalVehicles++;
        vehicleCount++;
    }

    public void accelerate(int increase) {
        speed += increase;
        System.out.println(modelName + " accelerated by " + increase + " km/h. New speed: " + speed + " km/h");
    }

    public void brake(int decrease) {
        if (speed - decrease < 0) {
            speed = 0;
        } else {
            speed -= decrease;
        }
        System.out.println(modelName + " slowed down by " + decrease + " km/h. New speed: " + speed + " km/h");
    }

    public void displayVehicleInfo() {
        System.out.println("Model: " + modelName + ", Speed: " + speed + " km/h");
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Enter the number of vehicles: ");
        int numVehicles = scanner.nextInt();
        scanner.nextLine();

        Vehicle[] vehicles = new Vehicle[numVehicles];
        
        for (int i = 0; i < numVehicles; i++) {
            System.out.print("Enter model name for vehicle " + (i + 1) + ": ");
            String modelName = scanner.nextLine();
            
            System.out.print("Enter initial speed for " + modelName + ": ");
            int speed = scanner.nextInt();
            scanner.nextLine();
            
            vehicles[i] = new Vehicle(modelName, speed);
        }

        System.out.println("\nTotal vehicles created: " + totalVehicles);
        
        for (int i = 0; i < vehicles.length; i++) {
            vehicles[i].displayVehicleInfo();
        }

        System.out.println("\nDo you want to modify vehicle speeds? (yes/no): ");
        String modify = scanner.nextLine();
        
        while (modify.equalsIgnoreCase("yes")) {
            System.out.print("Enter vehicle number to modify (1 to " + numVehicles + "): ");
            int vehicleIndex = scanner.nextInt() - 1;
            
            if (vehicleIndex >= 0 && vehicleIndex < numVehicles) {
                System.out.print("Enter 'A' to accelerate or 'B' to brake: ");
                char action = scanner.next().charAt(0);
                
                System.out.print("Enter the speed change value: ");
                int value = scanner.nextInt();
                scanner.nextLine();
                
                if (action == 'A' || action == 'a') {
                    vehicles[vehicleIndex].accelerate(value);
                } else if (action == 'B' || action == 'b') {
                    vehicles[vehicleIndex].brake(value);
                } else {
                    System.out.println("Invalid action.");
                }
            } else {
                System.out.println("Invalid vehicle number.");
            }
            
            System.out.println("\nDo you want to modify another vehicle? (yes/no): ");
            modify = scanner.nextLine();
        }
        
        System.out.println("\nFinal Vehicle Information:");
        for (int i = 0; i < vehicles.length; i++) {
            vehicles[i].displayVehicleInfo();
        }
        
        scanner.close();
    }
}
