// Source code is decompiled from a .class file using FernFlower decompiler (from Intellij IDEA).
import java.awt.BorderLayout;
import java.awt.CardLayout;
import java.awt.Color;
import java.awt.Component;
import java.awt.Dimension;
import java.awt.FlowLayout;
import java.awt.Font;
import java.awt.GridBagConstraints;
import java.awt.GridBagLayout;
import java.awt.Insets;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;
import java.util.Arrays;
import java.util.List;
import java.util.Objects;
import javax.swing.BorderFactory;
import javax.swing.ButtonGroup;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JPasswordField;
import javax.swing.JRadioButton;
import javax.swing.JScrollPane;
import javax.swing.JTextArea;
import javax.swing.JTextField;
import javax.swing.SwingUtilities;
import javax.swing.Timer;

public class ExaminationSystem extends JFrame {
   private static final long serialVersionUID = 1L;
   private static final int DURATION_SECONDS = 1800;
   private static final Color NAVY = new Color(20, 42, 74);
   private static final Color BLUE = new Color(34, 104, 180);
   private final CardLayout layout = new CardLayout();
   private final JPanel screens;
   private final User user;
   private final List<Question> questions;
   private final int[] answers;
   private final JTextField username;
   private final JPasswordField password;
   private final JTextField displayName;
   private final JPasswordField newPassword;
   private final JLabel timerLabel;
   private final JLabel numberLabel;
   private final JLabel questionLabel;
   private final JRadioButton[] options;
   private final ButtonGroup optionGroup;
   private final JTextArea result;
   private Timer timer;
   private int remaining;
   private int current;
   private long startedAt;
   private boolean examActive;

   public static void main(String[] var0) {
      if (var0.length > 0 && "--self-test".equals(var0[0])) {
         System.out.println("Online examination system is ready.");
      } else {
         SwingUtilities.invokeLater(() -> (new ExaminationSystem()).setVisible(true));
      }
   }

   public ExaminationSystem() {
      this.screens = new JPanel(this.layout);
      this.user = new User("student", "student123", "Aarav Sharma");
      this.questions = List.of(new Question("Which collection does not allow duplicate elements?", new String[]{"List", "Set", "Queue", "Map"}, 1), new Question("Which keyword is used to inherit a class in Java?", new String[]{"implements", "inherits", "extends", "super"}, 2), new Question("What is the default value of an int field in Java?", new String[]{"0", "null", "1", "undefined"}, 0), new Question("Which Swing component is used for a single-line text input?", new String[]{"JTextArea", "JLabel", "JTextField", "JEditorPane"}, 2), new Question("Which method starts a Java thread?", new String[]{"run()", "start()", "begin()", "execute()"}, 1), new Question("Which principle hides internal implementation details?", new String[]{"Inheritance", "Polymorphism", "Encapsulation", "Overloading"}, 2), new Question("What does SQL stand for?", new String[]{"Structured Query Language", "Simple Question Language", "System Query Logic", "Sequential Query List"}, 0), new Question("Which layout stacks components in rows and columns?", new String[]{"FlowLayout", "GridLayout", "BorderLayout", "CardLayout"}, 1));
      this.answers = new int[this.questions.size()];
      this.username = new JTextField(20);
      this.password = new JPasswordField(20);
      this.displayName = new JTextField(24);
      this.newPassword = new JPasswordField(24);
      this.timerLabel = new JLabel();
      this.numberLabel = new JLabel();
      this.questionLabel = new JLabel();
      this.options = new JRadioButton[4];
      this.optionGroup = new ButtonGroup();
      this.result = new JTextArea();
      this.setTitle("Online Examination System");
      this.setSize(820, 570);
      this.setMinimumSize(new Dimension(700, 500));
      this.setLocationRelativeTo((Component)null);
      this.setDefaultCloseOperation(0);
      this.addWindowListener(new WindowAdapter() {
         {
            Objects.requireNonNull(ExaminationSystem.this);
         }

         public void windowClosing(WindowEvent var1) {
            if (!ExaminationSystem.this.examActive || ExaminationSystem.this.confirm("Are you sure you want to quit?", "Quit examination", 2)) {
               ExaminationSystem.this.dispose();
            }

         }
      });
      this.screens.add(this.loginScreen(), "login");
      this.screens.add(this.profileScreen(), "profile");
      this.screens.add(this.examScreen(), "exam");
      this.screens.add(this.resultScreen(), "result");
      this.add(this.screens);
      this.layout.show(this.screens, "login");
   }

   private JPanel loginScreen() {
      JPanel var1 = new JPanel(new GridBagLayout());
      JPanel var2 = new JPanel(new GridBagLayout());
      var2.setBorder(BorderFactory.createCompoundBorder(BorderFactory.createLineBorder(new Color(210, 220, 232)), BorderFactory.createEmptyBorder(28, 34, 28, 34)));
      this.addTitle(var2, "Student Login", 0);
      addRow(var2, 2, "Username", this.username);
      addRow(var2, 3, "Password", this.password);
      JButton var3 = this.primary("Login");
      var3.addActionListener((var1x) -> this.login());
      GridBagConstraints var4 = constraints(4);
      var4.gridwidth = 2;
      var2.add(var3, var4);
      var1.add(var2);
      return var1;
   }

   private JPanel profileScreen() {
      JPanel var1 = this.content();
      JPanel var2 = new JPanel(new GridBagLayout());
      var2.setBorder(BorderFactory.createTitledBorder("Profile before exam"));
      addRow(var2, 0, "Display name", this.displayName);
      addRow(var2, 1, "New password", this.newPassword);
      JLabel var3 = new JLabel("Leave new password blank to keep the current password.");
      var3.setForeground(Color.DARK_GRAY);
      GridBagConstraints var4 = constraints(2);
      var4.gridwidth = 2;
      var2.add(var3, var4);
      JButton var5 = this.primary("Save profile and start exam");
      var5.addActionListener((var1x) -> this.startAfterProfile());
      JButton var6 = new JButton("Logout");
      var6.addActionListener((var1x) -> this.logout());
      JPanel var7 = new JPanel(new FlowLayout(2));
      var7.add(var6);
      var7.add(var5);
      var1.add(var2, "Center");
      var1.add(var7, "South");
      return var1;
   }

   private JPanel examScreen() {
      JPanel var1 = this.content();
      JPanel var2 = new JPanel(new BorderLayout());
      JLabel var3 = this.title("Online Examination");
      this.timerLabel.setFont(new Font("Monospaced", 1, 22));
      this.timerLabel.setForeground(new Color(174, 45, 45));
      var2.add(var3, "West");
      var2.add(this.timerLabel, "East");
      var1.add(var2, "North");
      JPanel var4 = new JPanel(new BorderLayout(12, 12));
      var4.setBorder(BorderFactory.createEmptyBorder(30, 20, 20, 20));
      this.questionLabel.setFont(new Font("SansSerif", 1, 18));
      JPanel var5 = new JPanel(new BorderLayout(0, 12));
      var5.add(this.numberLabel, "North");
      var5.add(this.questionLabel, "Center");
      JPanel var6 = new JPanel(new GridBagLayout());

      for(int var7 = 0; var7 < this.options.length; ++var7) {
         this.options[var7] = new JRadioButton();
         this.options[var7].setFont(new Font("SansSerif", 0, 16));
         this.optionGroup.add(this.options[var7]);
         GridBagConstraints var8 = constraints(var7);
         var8.fill = 2;
         var8.weightx = (double)1.0F;
         var6.add(this.options[var7], var8);
      }

      var4.add(var5, "North");
      var4.add(var6, "Center");
      var1.add(var4, "Center");
      JButton var11 = new JButton("Previous");
      var11.addActionListener((var1x) -> this.move(-1));
      JButton var12 = this.primary("Next");
      var12.addActionListener((var1x) -> this.move(1));
      JButton var9 = new JButton("Submit exam");
      var9.addActionListener((var1x) -> this.submitConfirm());
      JPanel var10 = new JPanel(new FlowLayout(2));
      var10.add(var11);
      var10.add(var12);
      var10.add(var9);
      var1.add(var10, "South");
      return var1;
   }

   private JPanel resultScreen() {
      JPanel var1 = this.content();
      var1.add(this.title("Examination Result"), "North");
      this.result.setEditable(false);
      this.result.setFont(new Font("Monospaced", 0, 14));
      var1.add(new JScrollPane(this.result), "Center");
      JButton var2 = new JButton("Logout");
      var2.addActionListener((var1x) -> this.logout());
      JPanel var3 = new JPanel(new FlowLayout(2));
      var3.add(var2);
      var1.add(var3, "South");
      return var1;
   }

   private void login() {
      if (this.user.username.equals(this.username.getText().trim()) && this.user.password.equals(new String(this.password.getPassword()))) {
         this.displayName.setText(this.user.displayName);
         this.newPassword.setText("");
         this.layout.show(this.screens, "profile");
      } else {
         JOptionPane.showMessageDialog(this, "Invalid username or password.", "Login failed", 0);
         this.password.setText("");
      }
   }

   private void startAfterProfile() {
      String var1 = this.displayName.getText().trim();
      String var2 = new String(this.newPassword.getPassword());
      if (var1.isEmpty()) {
         this.warning("Display name is required.");
      } else if (!var2.isEmpty() && var2.length() < 6) {
         this.warning("New password must contain at least 6 characters.");
      } else {
         this.user.displayName = var1;
         if (!var2.isEmpty()) {
            this.user.password = var2;
         }

         this.startExam();
      }
   }

   private void startExam() {
      Arrays.fill(this.answers, -1);
      this.current = 0;
      this.remaining = 1800;
      this.startedAt = System.currentTimeMillis();
      this.examActive = true;
      this.updateTimer();
      this.renderQuestion();
      this.timer = new Timer(1000, (var1) -> {
         --this.remaining;
         this.updateTimer();
         if (this.remaining <= 0) {
            this.finish(true);
         }

      });
      this.timer.start();
      this.layout.show(this.screens, "exam");
   }

   private void renderQuestion() {
      Question var1 = (Question)this.questions.get(this.current);
      int var10001 = this.current + 1;
      this.numberLabel.setText("Question " + var10001 + " of " + this.questions.size());
      this.questionLabel.setText("<html>" + var1.text + "</html>");
      this.optionGroup.clearSelection();

      for(int var2 = 0; var2 < this.options.length; ++var2) {
         this.options[var2].setText((char)(65 + var2) + ".  " + var1.options[var2]);
         this.options[var2].setSelected(this.answers[this.current] == var2);
      }

   }

   private void saveAnswer() {
      this.answers[this.current] = -1;

      for(int var1 = 0; var1 < this.options.length; ++var1) {
         if (this.options[var1].isSelected()) {
            this.answers[this.current] = var1;
            break;
         }
      }

   }

   private void move(int var1) {
      this.saveAnswer();
      int var2 = this.current + var1;
      if (var2 >= 0 && var2 < this.questions.size()) {
         this.current = var2;
         this.renderQuestion();
      }

   }

   private void submitConfirm() {
      this.saveAnswer();
      int var1 = 0;

      for(int var5 : this.answers) {
         if (var5 < 0) {
            ++var1;
         }
      }

      String var6 = var1 == 0 ? "Submit your exam now?" : "You have " + var1 + " unanswered question(s). Submit anyway?";
      if (this.confirm(var6, "Confirm submission", 3)) {
         this.finish(false);
      }

   }

   private void finish(boolean var1) {
      if (this.examActive) {
         this.saveAnswer();
         this.examActive = false;
         if (this.timer != null) {
            this.timer.stop();
         }

         int var2 = 0;
         int var3 = 0;
         int var4 = 0;
         StringBuilder var5 = new StringBuilder();

         for(int var6 = 0; var6 < this.questions.size(); ++var6) {
            Question var7 = (Question)this.questions.get(var6);
            int var8 = this.answers[var6];
            if (var8 == var7.correct) {
               ++var2;
               var5.append("Q").append(var6 + 1).append(": Correct\n");
            } else if (var8 < 0) {
               ++var4;
               var5.append("Q").append(var6 + 1).append(": Unanswered (correct: ").append(var7.options[var7.correct]).append(")\n");
            } else {
               ++var3;
               var5.append("Q").append(var6 + 1).append(": Incorrect (correct: ").append(var7.options[var7.correct]).append(")\n");
            }
         }

         long var9 = Math.min(1800L, Math.max(0L, (System.currentTimeMillis() - this.startedAt) / 1000L));
         this.result.setText((var1 ? "TIME UP - Your exam was submitted automatically.\n\n" : "Exam submitted successfully.\n\n") + "Student: " + this.user.displayName + "\nScore: " + var2 + " out of " + this.questions.size() + "\nCorrect: " + var2 + "    Incorrect: " + var3 + "    Unanswered: " + var4 + "\nTime taken: " + duration(var9) + "\n\nAnswer breakdown\n----------------\n" + String.valueOf(var5));
         this.layout.show(this.screens, "result");
      }
   }

   private void logout() {
      if (!this.examActive || this.confirm("Are you sure you want to quit?", "Quit examination", 2)) {
         if (this.timer != null) {
            this.timer.stop();
         }

         this.examActive = false;
         this.username.setText("");
         this.password.setText("");
         this.layout.show(this.screens, "login");
      }
   }

   private void updateTimer() {
      this.timerLabel.setText(duration((long)this.remaining));
   }

   private static String duration(long var0) {
      return String.format("%02d:%02d", var0 / 60L, var0 % 60L);
   }

   private boolean confirm(String var1, String var2, int var3) {
      return JOptionPane.showConfirmDialog(this, var1, var2, 0, var3) == 0;
   }

   private void warning(String var1) {
      JOptionPane.showMessageDialog(this, var1, "Profile validation", 2);
   }

   private JPanel content() {
      JPanel var1 = new JPanel(new BorderLayout(16, 16));
      var1.setBorder(BorderFactory.createEmptyBorder(24, 32, 24, 32));
      return var1;
   }

   private JLabel title(String var1) {
      JLabel var2 = new JLabel(var1);
      var2.setFont(new Font("SansSerif", 1, 25));
      var2.setForeground(NAVY);
      return var2;
   }

   private JButton primary(String var1) {
      JButton var2 = new JButton(var1);
      var2.setBackground(BLUE);
      var2.setForeground(Color.WHITE);
      var2.setFocusPainted(false);
      return var2;
   }

   private void addTitle(JPanel var1, String var2, int var3) {
      GridBagConstraints var4 = constraints(var3);
      var4.gridwidth = 2;
      var1.add(this.title(var2), var4);
   }

   private static void addRow(JPanel var0, int var1, String var2, Component var3) {
      GridBagConstraints var4 = constraints(var1);
      var4.gridx = 0;
      var4.anchor = 22;
      var0.add(new JLabel(var2 + ":"), var4);
      GridBagConstraints var5 = constraints(var1);
      var5.gridx = 1;
      var5.fill = 2;
      var5.weightx = (double)1.0F;
      var0.add(var3, var5);
   }

   private static GridBagConstraints constraints(int var0) {
      GridBagConstraints var1 = new GridBagConstraints();
      var1.gridy = var0;
      var1.insets = new Insets(8, 8, 8, 8);
      return var1;
   }

   private static class User {
      private final String username;
      private String password;
      private String displayName;

      User(String var1, String var2, String var3) {
         this.username = var1;
         this.password = var2;
         this.displayName = var3;
      }
   }

   private static record Question(String text, String[] options, int correct) {
   }
}
