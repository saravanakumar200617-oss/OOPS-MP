import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class MiniBankSwing extends JFrame implements ActionListener {
    private JTextField amountField;
    private JLabel balanceLabel;
    private double balance = 0.0;

    public MiniBankSwing() {
        // Frame setup
        setTitle("Mini Banking System - Swing");
        setSize(400, 300);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);
        setLayout(new GridLayout(6, 1, 10, 10));

        // Title
        JLabel titleLabel = new JLabel("Mini Banking System", SwingConstants.CENTER);
        titleLabel.setFont(new Font("Arial", Font.BOLD, 18));
        add(titleLabel);

        // Amount input
        add(new JLabel("Enter Amount:", SwingConstants.CENTER));
        amountField = new JTextField();
        add(amountField);

        // Buttons
        JPanel buttonPanel = new JPanel();
        JButton depositBtn = new JButton("Deposit");
        JButton withdrawBtn = new JButton("Withdraw");
        JButton balanceBtn = new JButton("Check Balance");
        buttonPanel.add(depositBtn);
        buttonPanel.add(withdrawBtn);
        buttonPanel.add(balanceBtn);
        add(buttonPanel);

        // Balance label
        balanceLabel = new JLabel("Current Balance: ₹0.0", SwingConstants.CENTER);
        balanceLabel.setFont(new Font("Arial", Font.PLAIN, 16));
        add(balanceLabel);

        // Button listeners
        depositBtn.addActionListener(this);
        withdrawBtn.addActionListener(this);
        balanceBtn.addActionListener(this);

        setVisible(true);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        String command = e.getActionCommand();
        try {
            if (command.equals("Deposit")) {
                double amount = Double.parseDouble(amountField.getText());
                if (amount > 0) {
                    balance += amount;
                    balanceLabel.setText("Amount Deposited! Current Balance: ₹" + balance);
                } else {
                    JOptionPane.showMessageDialog(this, "Enter a valid amount!");
                }
            } else if (command.equals("Withdraw")) {
                double amount = Double.parseDouble(amountField.getText());
                if (amount > 0 && amount <= balance) {
                    balance -= amount;
                    balanceLabel.setText("Amount Withdrawn! Current Balance: ₹" + balance);
                } else {
                    JOptionPane.showMessageDialog(this, "Insufficient Balance or Invalid Amount!");
                }
            } else if (command.equals("Check Balance")) {
                JOptionPane.showMessageDialog(this, "Your Current Balance: ₹" + balance);
            }
            amountField.setText("");
        } catch (NumberFormatException ex) {
            JOptionPane.showMessageDialog(this, "Please enter a number!");
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new MiniBankSwing());
    }
}# OOPS-MP
