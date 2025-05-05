# Mini-project-
Applet code


import java.awt.*;
import java.awt.event.*;

class LoginException extends Exception {
    public LoginException(String message) {
        super(message);
    }
}

public class LoginScreen extends Frame implements ActionListener {
    Label l1, l2, message;
    TextField t1, t2;
    Button loginButton, clearButton;
    int attempts = 0;

    LoginScreen() {
        setLayout(new FlowLayout());

        l1 = new Label("Username:");
        t1 = new TextField(20);
        l2 = new Label("Password:");
        t2 = new TextField(20);
        t2.setEchoChar('*');

        loginButton = new Button("Login");
        clearButton = new Button("Clear");
        message = new Label();

        add(l1);
        add(t1);
        add(l2);
        add(t2);
        add(loginButton);
        add(clearButton);
        add(message);

        loginButton.addActionListener(this);
        clearButton.addActionListener(this);

        setTitle("Login Screen");
        setSize(300, 200);
        setVisible(true);

        addWindowListener(new WindowAdapter() {
            public void windowClosing(WindowEvent we) {
                dispose();
            }
        });
    }

    public void actionPerformed(ActionEvent ae) {
        if (ae.getSource() == loginButton) {
            try {
                String username = t1.getText();
                String password = t2.getText();
                
                if (username.equals(password)) {
                    message.setText("Login Successful!");
                } else {
                    attempts++;
                    throw new LoginException("Username and Password must be the same! Attempts left: " + (3 - attempts));
                }

                if (attempts >= 3) {
                    loginButton.setEnabled(false);
                    message.setText("Maximum attempts exceeded!");
                }
            } catch (LoginException e) {
                message.setText(e.getMessage());
            }
        } else if (ae.getSource() == clearButton) {
            t1.setText("");
            t2.setText("");
            message.setText("");
        }
    }

    public static void main(String[] args) {
        new LoginScreen();
    }
}
