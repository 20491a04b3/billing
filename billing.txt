import java.util.HashMap;

public class BillSplitter {
    public static void main(String[] args) {
        // Service information
        String[][] services = {
            {"LUNCH", "2500", "BALAJI"},
            {"MOVIE TICKET", "1000", "ANAND"},
            {"TEA/COFFEE", "750", "CHAITHANYA", "DIVYA"}
        };

        // Create a HashMap to store the individual amounts
        HashMap<String, Integer> individualAmounts = new HashMap<String, Integer>();
        individualAmounts.put("ANAND", 0);
        individualAmounts.put("BALAJI", 0);
        individualAmounts.put("CHAITHANYA", 0);
        individualAmounts.put("DIVYA", 0);

        // Loop through each service and update the individual amounts
        for (String[] service : services) {
            int bill = Integer.parseInt(service[1]);
            String paidBy = service[2];

            // Calculate the share for each individual
            int numPeople = service.length - 2;
            int share = bill / numPeople;

            // Update the individual amounts for the people who are interested
            for (int i = 2; i < service.length; i++) {
                String person = service[i];
                if (!person.equals(paidBy)) {
                    individualAmounts.put(person, individualAmounts.get(person) + share);
                }
            }

            // Add the total amount to the paidBy person
            individualAmounts.put(paidBy, individualAmounts.get(paidBy) + bill);
        }

        // Print the total amount for each service
        System.out.println("Total Amount for Each Service:");
        for (String[] service : services) {
            int bill = Integer.parseInt(service[1]);
            System.out.println(service[0] + ": " + bill);
        }

        // Print the total amount for each individual
        System.out.println("Total Amount for Each Individual:");
        for (String person : individualAmounts.keySet()) {
            System.out.println(person + ": " + individualAmounts.get(person));
        }

        // Calculate the amount each person needs to pay or receive
        System.out.println("Amounts to Pay/Receive:");
        for (String person1 : individualAmounts.keySet()) {
            for (String person2 : individualAmounts.keySet()) {
                if (!person1.equals(person2)) {
                    int amount1 = individualAmounts.get(person1);
                    int amount2 = individualAmounts.get(person2);
                    int diff = amount1 - amount2;
                    if (diff > 0) {
                        System.out.println(person1 + " needs to receive " + diff + " from " + person2);
                    } else if (diff < 0) {
                        System.out.println(person1 + " needs to pay " + (-diff) + " to " + person2);
                    }
                }
            }
        }
    }
}
