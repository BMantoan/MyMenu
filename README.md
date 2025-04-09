package menu;

import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.io.FileWriter;
import java.io.IOException;
import java.time.LocalDateTime;
import java.util.Random;

public class MyMenu extends JFrame {
    private JTextArea textArea;
    private final String[] orangeHues = {
        "#ff9980", "#ff8566", "#ff704d", "#ff5c33", "#ff471a",
        "#ff3300", "#e62e00", "#cc2900", "#b32400", "#991f00"
    };

    public MyMenu() {
        setupFrame();
        initializeTextArea();
        setupMenu();
    }

    private void setupFrame() {
        setTitle("Menu GUI");
        setSize(500, 300);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);
        setLayout(new BorderLayout());
    }
//initial Menu popup
    private void initializeTextArea() {
        textArea = new JTextArea();
        textArea.setText("Welcome! Select an option from the menu.\n");
        add(new JScrollPane(textArea), BorderLayout.CENTER);
    }
//Adds a option
    private void setupMenu() {
        JMenuBar menuBar = new JMenuBar();
        JMenu menu = new JMenu("Options");
//Option Classes
        JMenuItem showDateTime = new JMenuItem("Show Date/Time");
        JMenuItem saveToFile = new JMenuItem("Save to log.txt");
        JMenuItem changeColor = new JMenuItem("Random Orange Hue");
        JMenuItem exitApp = new JMenuItem("Exit");
//ActionListeners
        showDateTime.addActionListener(e -> showDateTime());
        saveToFile.addActionListener(e -> saveTextToFile());
        changeColor.addActionListener(e -> changeBackgroundColor());
        exitApp.addActionListener(e -> System.exit(0));

        menu.add(showDateTime);
        menu.add(saveToFile);
        menu.add(changeColor);
        menu.add(exitApp);

        menuBar.add(menu);
        setJMenuBar(menuBar);
    }
//Shows Current Date
    private void showDateTime() {
        LocalDateTime now = LocalDateTime.now();
        textArea.append("Current Date/Time: " + now + "\n");
    }
//Shows Saved File
    private void saveTextToFile() {
        try (FileWriter writer = new FileWriter("log.txt", true)) {
            writer.write(textArea.getText());
            textArea.append("Saved to log.txt\n");
        } catch (IOException ex) {
            textArea.append("Error writing to file.\n");
        }
    }
//Change Background Color
    private void changeBackgroundColor() {
        Random rand = new Random();
        String hex = orangeHues[rand.nextInt(orangeHues.length)];
        Color randomOrange = Color.decode(hex);
        getContentPane().setBackground(randomOrange);
        textArea.setBackground(randomOrange);
        textArea.append("Changed background to: " + hex + "\n");
        revalidate();
        repaint();
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new MyMenu().setVisible(true));
    }
}

