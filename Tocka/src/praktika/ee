package praktika;

import java.awt.Graphics; 
import java.awt.Image; 
import java.awt.event.MouseAdapter; 
import java.awt.event.MouseEvent; 
import java.io.IOException; 
import javax.imageio.ImageIO; 
import javax.swing.JFrame; 
import javax.swing.JPanel; 
import javax.swing.WindowConstants; 
 
public class Game extends JFrame { 
 
    private static Game game_game; 
    private static long last_frame_time; 
    private static Image kryg; 
    private static Image yx; 
    private static Image lb; 
    private static Image platforma; 
    private static float drop_left = 200; 
    private static float drop_top = 10; 
    private static float drop_v = 200; 
    private static int score = 0;  
 
    public static void main(String[] args) throws IOException { 
    
        yx = ImageIO.read(Game.class.getResourceAsStream("yx.png")); 
        Image krygOriginal = ImageIO.read(Game.class.getResourceAsStream("kryg.png")); 
        lb = ImageIO.read(Game.class.getResourceAsStream("lb.jpg")); 
        platforma = ImageIO.read(Game.class.getResourceAsStream("platforma.jpg"));  
 
        
        kryg = krygOriginal.getScaledInstance( 
            krygOriginal.getWidth(null) / 2,  
            krygOriginal.getHeight(null) / 2,  
            Image.SCALE_SMOOTH 
        ); 
 
        game_game = new Game(); 
        game_game.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE); 
        game_game.setLocation(200, 50); 
        game_game.setSize(1520, 800); 
        game_game.setResizable(false); 
        last_frame_time = System.nanoTime(); 
         
        GameField game_field = new GameField(); 
        game_game.add(game_field); 
        game_game.setVisible(true); 
 
         
        game_field.addMouseListener(new MouseAdapter() { 
            @Override 
            public void mousePressed(MouseEvent e) { 
                int x = e.getX(); 
                int y = e.getY(); 
 
                float drop_right = drop_left + platforma.getWidth(null); 
                float drop_bottom = drop_top + platforma.getHeight(null); 
                boolean is_drop = x >= drop_left && x <= drop_right && y >= drop_top && y <= drop_bottom; 
 
                if (is_drop) { 
                    drop_top = -100; 
                    drop_left = (int) (Math.random() * (game_field.getWidth() - platforma.getWidth(null))); 
                    drop_v += 10; 
                    score++;  
                    game_game.setTitle("Score: " + score); 
                } 
            } 
        }); 
    } 
 
    public static void onRepaint(Graphics g) { 
        long current_time = System.nanoTime(); 
        float delta_time = (current_time - last_frame_time) / 1_000_000_000.0f;  
        last_frame_time = current_time; 
 
        drop_top += drop_v * delta_time;  
 
        g.drawImage(lb, 0, 0, null); 
        g.drawImage(yx, 850, 150, 600, 600, null); 
        g.drawImage(kryg, (int) drop_left, (int) drop_top, null); 
 
        if (drop_top > game_game.getHeight()) { 
            g.drawImage(platforma, 210, 150, null); 
           
        } 
    } 
 
    public static class GameField extends JPanel { 
       
         private static Game lb;
          private static Image kryg;
            private static Image platforma; 
             @Override 
        protected void paintComponent(Graphics g) { 
            super.paintComponent(g); 
            onRepaint(g); 
            repaint(); 
        } 
    } 
}