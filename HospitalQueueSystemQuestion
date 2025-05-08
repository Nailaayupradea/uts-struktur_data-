
import java.util.ArrayList; //digunakan untuk mengimpor kelas ArrayList.
import java.util.Scanner; //digunakan untuk membaca input dari pengguna.

public class HospitalQueueSystemQuestion { //

    private static ArrayList<Patient> patientQueue = new ArrayList<>(); //membuat antrian pasien (ArrayList).
    private static Scanner scanner = new Scanner(System.in); // digunakan untuk mendeklarasikan sebuah objek Scanner.

    public static void main(String[] args) {
        boolean running = true; //untuk menjalankan program (looping menu utama).

        System.out.println("Welcome to Hospital Queue Management System"); //menampilkan pesan.

        while (running) { //selama program berjalan.
            displayMenu(); //menampilkan menu pilihan.
            int choice = getValidIntInput("Enter your choice: "); //membaca input.

            switch (choice) {
                case 1:
                    addPatient(); //menambah pasien baru.
                    break;
                case 2:
                    serveNextPatient(); //melayani pasien berikutnya.
                    break;
                case 3:
                    displayQueue(); //menampilkan antrian pasien saat ini.
                    break;
                case 4:
                    updatePriority(); //memperbarui prioritas pasien.
                    break;
                case 5:
                    searchPatient(); //mencari pasien dalam antrian.
                    break;
                case 6:
                    System.out.println("Thank you for using Hospital Queue Management System. Goodbye!"); //menampilkan pesan.
                    running = false; //menghentikan program.
                    break;
                default:
                    System.out.println("Invalid choice. Please try again."); //menampilkan pesan jika tidak valid.
            }
        }

        scanner.close(); //menutup objek scanner.
    }

    private static void displayMenu() {
        //menampilkan menu pilihan.
        System.out.println("\n===== HOSPITAL QUEUE SYSTEM =====");
        System.out.println("1. Add a new patient to the queue");
        System.out.println("2. Serve next patient");
        System.out.println("3. Display current queue");
        System.out.println("4. Update patient priority");
        System.out.println("5. Search for a patient");
        System.out.println("6. Exit");
        System.out.println("=================================");
    }

    //mengambil data pasien dari input pengguna, menentukan posisi insert berdasarkan prioritas (semakin kecil nilai, semakin tinggi prioritas), menambahkan pasien ke antrean pada posisi yang sesuai.
    private static void addPatient() {
        System.out.println("\n--- Add New Patient ---");
        String name = getValidStringInput("Enter patient's name: ");
        int age = getValidIntInput("Enter patient's age: ");
        String condition = getValidStringInput("Enter condition description: ");
        int priority = getValidIntInRange("Enter priority (1-Critical to 5-Non-urgent): ", 1, 5);

        Patient newPatient = new Patient(name, age, condition, priority);
        int index = 0;
        while (index < patientQueue.size() && patientQueue.get(index).getPriority() <= priority) {
            index++;
        }
        patientQueue.add(index, newPatient);
        System.out.println("Patient added successfully.");
    }

    //mengambil dan menghapus pasien pertama dari antrean (prioritas tertinggi), menampilkan data pasien yang sedang dilayani.
    private static void serveNextPatient() {
        if (patientQueue.isEmpty()) {
            System.out.println("No patients in queue.");
        } else {
            Patient next = patientQueue.remove(0);
            System.out.println("Serving patient: " + next.getName()
                    + " | Age: " + next.getAge()
                    + " | Condition: " + next.getCondition()
                    + " | Priority: " + getPriorityText(next.getPriority()));
        }
    }

    //menampilkan seluruh pasien dalam antrean beserta detailnya.
    private static void displayQueue() {
        if (patientQueue.isEmpty()) {
            System.out.println("No patients in queue.");
        } else {
            System.out.println("\n--- Current Patient Queue ---");
            for (int i = 0; i < patientQueue.size(); i++) {
                Patient p = patientQueue.get(i);
                System.out.println((i + 1) + ". " + p.getName()
                        + " | Age: " + p.getAge()
                        + " | Condition: " + p.getCondition()
                        + " | Priority: " + getPriorityText(p.getPriority()));
            }
        }
    }

    //mencari pasien jika ditemukan maka dapat menghapus antrean, ubah prioritas, dan menambahkan ke antrean berdasarkan prioritas baru. jika kosong maka keluar dari fungsi.
    private static void updatePriority() {
        if (patientQueue.isEmpty()) {
            System.out.println("No patients to update.");
            return;
        }

        String name = getValidStringInput("Enter the patient's name to update: ");
        boolean found = false;

        for (int i = 0; i < patientQueue.size(); i++) {
            Patient p = patientQueue.get(i);
            if (p.getName().equalsIgnoreCase(name)) {
                int newPriority = getValidIntInRange("Enter new priority (1-Critical to 5-Non-urgent): ", 1, 5);
                patientQueue.remove(i);
                p.setPriority(newPriority);

                int index = 0;
                while (index < patientQueue.size() && patientQueue.get(index).getPriority() <= newPriority) {
                    index++;
                }
                patientQueue.add(index, p);
                System.out.println("Priority updated successfully.");
                found = true;
                break;
            }
        }

        if (!found) {
            System.out.println("Patient not found.");
        }
    }

    //mencari pasien dalam antrean dan menampilkan jika ditemukan.
    private static void searchPatient() {
        if (patientQueue.isEmpty()) {
            System.out.println("No patients in queue.");
            return;
        }

        String name = getValidStringInput("Enter the patient's name to search: ");
        boolean found = false;

        for (Patient p : patientQueue) {
            if (p.getName().equalsIgnoreCase(name)) {
                System.out.println("Found: " + p.getName()
                        + " | Age: " + p.getAge()
                        + " | Condition: " + p.getCondition()
                        + " | Priority: " + getPriorityText(p.getPriority()));
                found = true;
                break;
            }
        }

        if (!found) {
            System.out.println("Patient not found.");
        }
    }

    private static String getPriorityText(int priority) {
        switch (priority) {
            case 1:
                return "1-Critical"; //prioritas 1 - kritis.
            case 2:
                return "2-Urgent"; //prioritas 2 - mendesak.
            case 3:
                return "3-High"; //prioritas 3 - tinggi.
            case 4:
                return "4-Medium"; //prioritas 4 - sedang.
            case 5:
                return "5-Non-urgent"; //prioritas 5 - tidak mendesak.
            default:
                return "Unknown"; //prioritas tidak valid.
        }
    }

    //meminta input angka dari user. Akan terus mengulang hingga input yang diberikan adalah angka valid (integer).
    private static int getValidIntInput(String prompt) {
        int value;
        while (true) {
            System.out.print(prompt);
            try {
                value = Integer.parseInt(scanner.nextLine().trim());
                break;
            } catch (NumberFormatException e) {
                System.out.println("Invalid input. Please enter a number.");
            }
        }
        return value;
    }

    //memastikan bahwa angka yang dimasukkan berada dalam rentang tertentu (termasuk batas).
    private static int getValidIntInRange(String prompt, int min, int max) {
        int value;
        while (true) {
            value = getValidIntInput(prompt);
            if (value >= min && value <= max) {
                break;
            }
            System.out.println("Please enter a value between " + min + " and " + max + ".");
        }
        return value;
    }

    //meminta input teks (string) dari user dan memastikan input tersebut tidak kosong.
    private static String getValidStringInput(String prompt) {
        String value;
        while (true) {
            System.out.print(prompt);
            value = scanner.nextLine().trim();
            if (!value.isEmpty()) {
                break;
            }
            System.out.println("Input cannot be empty. Please try again.");
        }
        return value;
    }
}

class Patient {

    private String name; //nama pasien.
    private int age; //umur pasien.
    private String condition; //kondisi pasien.
    private int priority; // 1 (Critical) to 5 (Non-urgent)

    public Patient(String name, int age, String condition, int priority) {
        this.name = name; //inisialisasi nama pasien.
        this.age = age; //inisialisasi umur pasien.
        this.condition = condition; //inisialisasi kondisi pasien.
        this.priority = priority; //inisialisasi prioritas pasien.
    }

    public String getName() {
        return name; //mengembalikan nama pasien.
    }

    public int getAge() {
        return age; //mengembalikan umur pasien.
    }

    public String getCondition() {
        return condition; // mengembalikan kondisi pasien.
    }

    public int getPriority() {
        return priority; //mengembalikan prioritas pasien.
    }

    public void setPriority(int priority) {
        this.priority = priority; //mengatur prioritas pasien.
    }
}
