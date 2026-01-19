package customerregistration;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.ArrayList;
import java.util.List;

/**
 * Class 1 & 2: Person & Customer (OOP Principles)
 */
class Person {
    protected String name;
    public Person(String name) { this.name = name; }
}

class Customer extends Person {
    private String id;
    private String phone;

    public Customer(String id, String name, String phone) {
        super(name);
        this.id = id;
        this.phone = phone;
    }

    public String getId() { return id; } // ميثود ضرورية لعملية البحث

    @Override
    public String toString() {
        return "ID: " + id + " | Name: " + name + " | Phone: " + phone;
    }
}

/**
 * Class 3: CustomerManager
 * يحتوي على خوارزمية البحث الخطي (Linear Search Algorithm)[cite: 91, 113].
 */
class CustomerManager {
    private List<Customer> customerList = new ArrayList<>();

    public void addCustomer(String id, String name, String phone) {
        customerList.add(new Customer(id, name, phone));
    }

    // --- تطبيق خوارزمية البحث الخطي --- [cite: 96, 118]
    public Customer searchById(String id) {
        for (Customer c : customerList) { // تمر الخوارزمية على كل عنصر في القائمة
            if (c.getId().equals(id)) {  // مقارنة المعرف المطلوب بمعرف العميل الحالي
                return c; // نجاح البحث: إرجاع الكائن المكتشف
            }
        }
        return null; // فشل البحث: المعرف غير موجود
    }

    public List<Customer> getList() { return customerList; }
}

/**
 * Class 4: CustomerRegistration (UI & Events)
 */
public class CustomerRegistration extends JFrame {
    private CustomerManager manager = new CustomerManager();
    private JTextField txtID = new JTextField(15);
    private JTextField txtName = new JTextField(15);
    private JTextField txtPhone = new JTextField(15);
    private DefaultListModel<String> listModel = new DefaultListModel<>();
    private JList<String> customerJList = new JList<>(listModel);

    public CustomerRegistration() {
        setTitle("Zain Jordan - CIMS (Linear Search Implementation)");
        setSize(500, 500);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new BorderLayout(15, 15));

        JPanel pnlInput = new JPanel(new GridLayout(5, 2, 10, 10));
        pnlInput.setBorder(BorderFactory.createTitledBorder("Registration & Search"));
        
        pnlInput.add(new JLabel("Customer ID:"));
        pnlInput.add(txtID);
        pnlInput.add(new JLabel("Full Name:"));
        pnlInput.add(txtName);
        pnlInput.add(new JLabel("Phone Number:"));
        pnlInput.add(txtPhone);

        JButton btnAdd = new JButton("Register Customer");
        JButton btnSearch = new JButton("Search by ID"); // زر جديد لتفعيل البحث
        pnlInput.add(btnAdd);
        pnlInput.add(btnSearch);

        add(pnlInput, BorderLayout.NORTH);
        add(new JScrollPane(customerJList), BorderLayout.CENTER);

        // حدث الإضافة
        btnAdd.addActionListener(e -> {
            String id = txtID.getText().trim();
            String name = txtName.getText().trim();
            String phone = txtPhone.getText().trim();

            if (id.isEmpty() || name.isEmpty()) {
                JOptionPane.showMessageDialog(this, "Please enter ID and Name.");
                return;
            }
            manager.addCustomer(id, name, phone);
            listModel.addElement("Added: " + name + " (ID: " + id + ")");
            clearFields();
        });

        // --- حدث البحث (استدعاء خوارزمية Linear Search) --- [cite: 101, 128]
        btnSearch.addActionListener(e -> {
            String searchID = txtID.getText().trim();
            if (searchID.isEmpty()) {
                JOptionPane.showMessageDialog(this, "Enter ID to search.");
                return;
            }

            Customer result = manager.searchById(searchID); // استدعاء الخوارزمية
            if (result != null) {
                JOptionPane.showMessageDialog(this, "Customer Found:\n" + result.toString());
            } else {
                JOptionPane.showMessageDialog(this, "Customer ID not found in Zain records.");
            }
        });
    }

    private void clearFields() {
        txtID.setText(""); txtName.setText(""); txtPhone.setText("");
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new CustomerRegistration().setVisible(true));
    }
}