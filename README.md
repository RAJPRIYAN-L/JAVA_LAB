import java.util.Scanner;

class ElectricityBill {
    int consumerNo;
    String consumerName;
    int previousReading;
    int currentReading;
    String connectionType;
    double billAmount;

    void getDetails() {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter Consumer Number: ");
        consumerNo = sc.nextInt();
        sc.nextLine();

        System.out.print("Enter Consumer Name: ");
        consumerName = sc.nextLine();

        System.out.print("Enter Previous Meter Reading: ");
        previousReading = sc.nextInt();

        System.out.print("Enter Current Meter Reading: ");
        currentReading = sc.nextInt();
        sc.nextLine();

        System.out.print("Enter Connection Type (DOMESTIC/COMMERCIAL): ");
        connectionType = sc.nextLine().toUpperCase();
    }

    void calculateBill() {
        int units = currentReading - previousReading;

        if (connectionType.equals("DOMESTIC")) {

            if (units <= 100) {
                billAmount = 0;
            } else if (units <= 200) {
                billAmount = (units - 100) * 2;
            } else if (units <= 500) {
                billAmount = (100 * 2) + (units - 200) * 4;
            } else {
                billAmount = (100 * 2) + (300 * 4) + (units - 500) * 6;
            }

        } else if (connectionType.equals("COMMERCIAL")) {

            if (units <= 100) {
                billAmount = units * 2;
            } else if (units <= 200) {
                billAmount = (100 * 2) + (units - 100) * 4;
            } else if (units <= 500) {
                billAmount = (100 * 2) + (100 * 4) + (units - 200) * 6;
            } else {
                billAmount = (100 * 2) + (100 * 4) + (300 * 6) + (units - 500) * 7;
            }

        } else {
            System.out.println("Invalid Connection Type");
        }
    }

    void displayBill() {
        System.out.println("\n----- Electricity Bill -----");
        System.out.println("Consumer Number : " + consumerNo);
        System.out.println("Consumer Name   : " + consumerName);
        System.out.println("Connection Type : " + connectionType);
        System.out.println("Units Consumed  : " + (currentReading - previousReading));
        System.out.println("Bill Amount     : Rs. " + billAmount);
    }

    public static void main(String[] args) {
        ElectricityBill eb = new ElectricityBill();
        eb.getDetails();
        eb.calculateBill();
        eb.displayBill();
    }
}
