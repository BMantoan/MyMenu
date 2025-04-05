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
        setTitle("Menu GUI");
        setSize(500, 300);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);

        textArea = new JTextArea();
        textArea.setText("Welcome! Select an option from the menu.\n"); // Default text 
        add(new JScrollPane(textArea), BorderLayout.CENTER);

        JMenuBar menuBar = new JMenuBar();
        JMenu menu = new JMenu("Options");

        JMenuItem showDateTime = new JMenuItem("Show Date/Time");
        JMenuItem saveToFile = new JMenuItem("Save to log.txt");
        JMenuItem changeColor = new JMenuItem("Random Orange Hue");
        JMenuItem exitApp = new JMenuItem("Exit");

        menu.add(showDateTime);
        menu.add(saveToFile);
        menu.add(changeColor);
        menu.add(exitApp);
        menuBar.add(menu);
        setJMenuBar(menuBar);

        showDateTime.addActionListener(e -> {
            LocalDateTime now = LocalDateTime.now();
            textArea.append("Current Date/Time: " + now + "\n");
        });

        saveToFile.addActionListener(e -> {
            try (FileWriter writer = new FileWriter("log.txt", true)) {
                writer.write(textArea.getText());
                textArea.append("Saved to log.txt\n");
            } catch (IOException ex) {
                textArea.append("Error writing to file.\n");
            }
        });

        changeColor.addActionListener(e -> {
            Random rand = new Random();
            String hex = orangeHues[rand.nextInt(orangeHues.length)];
            Color randomOrange = Color.decode(hex);
            getContentPane().setBackground(randomOrange);
            textArea.setBackground(randomOrange);
            revalidate();
            repaint(); //Paints the background	
            textArea.append("Changed background to: " + hex + "\n");
        });

        exitApp.addActionListener(e -> System.exit(0));
    }

    public static void main(String[] args) {
        javax.swing.SwingUtilities.invokeLater(() -> new MyMenu().setVisible(true));
    }
}
