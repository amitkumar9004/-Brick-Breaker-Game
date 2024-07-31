# -Brick-Breaker-Game
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class BrickBreaker extends JFrame {
    private GamePanel gamePanel;

    public BrickBreaker() {
        initUI();
    }

    private void initUI() {
        gamePanel = new GamePanel();
        add(gamePanel);

        setTitle("Brick Breaker");
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        setSize(800, 600);
        setLocationRelativeTo(null);
    }

    public static void main(String[] args) {
        EventQueue.invokeLater(() -> {
            BrickBreaker game = new BrickBreaker();
            game.setVisible(true);
        });
    }
}

class GamePanel extends JPanel implements ActionListener, KeyListener {
    private Timer timer;
    private int score;
    private Paddle paddle;
    private Ball ball;
    private Brick[][] bricks;

    public GamePanel() {
        initGame();
    }

    private void initGame() {
        setFocusable(true);
        setBackground(Color.BLACK);
        setDoubleBuffered(true);

        paddle = new Paddle();
        ball = new Ball();
        bricks = new Brick[5][10]; // example size

        // Initialize bricks
        for (int i = 0; i < bricks.length; i++) {
            for (int j = 0; j < bricks[i].length; j++) {
                bricks[i][j] = new Brick(50 + j * 60, 30 + i * 20);
            }
        }

        addKeyListener(this);

        timer = new Timer(10, this);
        timer.start();
    }

    @Override
    public void paintComponent(Graphics g) {
        super.paintComponent(g);
        drawObjects(g);
    }

    private void drawObjects(Graphics g) {
        paddle.draw(g);
        ball.draw(g);

        for (int i = 0; i < bricks.length; i++) {
            for (int j = 0; j < bricks[i].length; j++) {
                if (!bricks[i][j].isDestroyed()) {
                    bricks[i][j].draw(g);
                }
            }
        }

        Toolkit.getDefaultToolkit().sync();
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        updateGame();
        repaint();
    }

    private void updateGame() {
        paddle.move();
        ball.move();
        checkCollisions();
    }

    private void checkCollisions() {
        // Implement collision detection logic
    }

    @Override
    public void keyPressed(KeyEvent e) {
        paddle.keyPressed(e);
    }

    @Override
    public void keyReleased(KeyEvent e) {
        paddle.keyReleased(e);
    }

    @Override
    public void keyTyped(KeyEvent e) {
        // Not used
    }
}

// Define Paddle, Ball, Brick classes with appropriate methods and attributes
