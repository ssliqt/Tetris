# Tetris
java project
package Main;


import Control.GameControl;
import dto.GameDto;

import javax.sound.sampled.AudioInputStream;
import javax.sound.sampled.AudioSystem;
import javax.sound.sampled.Clip;
import javax.sound.sampled.FloatControl;
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.File;
import java.util.ArrayList;
import java.io.IOException;
import java.io.PrintWriter;
import java.util.Scanner;


public class Main extends JFrame {
    //定义出主窗体
    private static Main main;
    private static ArrayList<JPanel> panels = new ArrayList<>();
    private static Color panelPen = Color.GRAY;
    private static Color shapePen = Color.RED;
    private static final Tuple blockSize = new Tuple(40, 40);
    private static final Tuple frameSize = new Tuple(800, 800);


    public static void main(String[] args) {
        //new出主窗体,初始化窗体
        main = new Main();
        main.initiateFrame("Tetris", frameSize);

        playMusic();

        //面板、按钮部分  根据需求进行按钮、面板的修改！！！！！！！！
        JPanel panel = initiatePanel(new Tuple(400, 400), panelPen);
        panel.add(new JLabel("This is panel1"));
        JPanel panel2 = initiatePanel(new Tuple(400, 400), panelPen);
        panel2.add(new JLabel("This is panel2"));
        JPanel panel4 = initiatePanel(new Tuple(400, 400), panelPen);
        panel4.add(new JLabel("This is panel4,to select an archive"));
        //GamePanel gamePanel = new GamePanel();
        main.addPanel(panel);


        JButton button = new JButton("PLAY");
        JButton button2 = new JButton("Return");
        JButton button3 = new JButton("New Game");
        JButton button5 = new JButton("Load");
        JButton button6 = new JButton("Return");

        //设置字体
        Font f = new Font("Adele",Font.PLAIN,15);

        //设置按钮字体
        button.setFont(f);
        button2.setFont(f);
        button3.setFont(f);
        button5.setFont(f);
        button6.setFont(f);
        //设置字体的颜色
        button.setForeground(Color.RED);
//
//            //TODO
//        });
        button.addActionListener(event -> main.setPanel((JPanel) button.getParent(), panel2));
        button2.addActionListener(event -> main.setPanel((JPanel) button2.getParent(), panel));
        button5.addActionListener(event -> main.setPanel((JPanel) button5.getParent(), panel4));
        button6.addActionListener(event -> main.setPanel((JPanel) button6.getParent(), panel2));

        button3.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                GameControl gameControl=new GameControl();
            }
        });

        //绝对布局 还要调整（根据最后大小)
        panel.setLayout(null);
        panel2.setLayout(null);
        //panel3.setLayout(null);

        button.setLocation(150,20);
        button.setSize(100,20);
        button2.setLocation(150,20);
        button2.setSize(100,20);
        button3.setLocation(150,50);
        button3.setSize(100,20);
        //button4.setLocation(150,20);
        button5.setLocation(150,80);
        button5.setSize(100,20);





        //把按钮加到面板上去
        panel.add(button);
        panel2.add(button2);
        panel2.add(button3);
        panel2.add(button5);
        panel4.add(button6);


        //设置窗体的背景
        /*ImageIcon image = new ImageIcon("D:\\JAVA\\game\\bj1.png");
        JLabel jlable = new JLabel(image);

        // 创建一个JLayeredPane用于分层的。
        JLayeredPane layeredPane = new JLayeredPane();
        JLayeredPane layeredPane1 = new JLayeredPane();
        JLayeredPane layeredPane2 = new JLayeredPane();

// 设置JPanel大小为背景图片大小
        panel.setBounds(0,0,image.getIconWidth(),image.getIconHeight());
        panel.add(jlable);

        panel2.setBounds(0,0,image.getIconWidth(),image.getIconHeight());
        panel2.add(jlable);

        panel4.setBounds(0,0,image.getIconWidth(),image.getIconHeight());
        panel4.add(jlable);

        //将jpanel放到JLayeredPane的最底层
        layeredPane.add(panel,layeredPane.DEFAULT_LAYER);
        layeredPane.add(panel2,layeredPane1.DEFAULT_LAYER);
        layeredPane.add(panel4,layeredPane2.DEFAULT_LAYER);
//将button放到jpanel高一层的地方
        layeredPane.add(button,layeredPane.MODAL_LAYER);
        layeredPane.add(button2,layeredPane1.MODAL_LAYER);
        layeredPane.add(button3,layeredPane1.MODAL_LAYER);
        layeredPane.add(button5,layeredPane1.MODAL_LAYER);
        layeredPane.add(button6,layeredPane2.MODAL_LAYER);*/


        /*ImageIcon imageIcon = new ImageIcon("D:/JAVA/game/bj1.png");
        JLabel jLabel = new JLabel(imageIcon);
        jLabel.setBounds(0,0,imageIcon.getIconWidth(),imageIcon.getIconHeight());


        // 将内容面板设置为透明
        panel.setOpaque(false);
        panel2.setOpaque(false);
        panel4.setOpaque(false);
        // 将窗体自动生成的内容面板替换成透明的内容面板
        main.setContentPane(panel);
        main.setContentPane(panel2);
        main.setContentPane(panel4);


        // 在窗体的分层面板的最底层添加图片标签
        main.getLayeredPane().add(jLabel, new Integer(Integer.MIN_VALUE));*/






        //TODO


        //流式布局
        //panel.setLayout(new FlowLayout(FlowLayout.LEADING, 20, 20));
        //panel2.setLayout(new FlowLayout(FlowLayout.LEADING, 20, 20));
        //panel3.setLayout(new FlowLayout(FlowLayout.LEADING, 20, 20));
    }

    //初始化窗体的方法
    private void initiateFrame(String title, Tuple size) {
        new JFrame(title);
        //窗口标题
        setTitle(title);
        //窗口尺寸
        setSize(size.x, size.y);
        //绑定关闭
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        //可见
        setVisible(true);
        //设置窗口居中
        setLocationRelativeTo(null);
        //this.setLayeredPane(layeredPane);
        //setSize(image.getIconWidth(),image.getIconHeight());

    }

    //初始化面板的方法  颜色
    private static JPanel initiatePanel(Tuple size, Color color) {
        JPanel panel = new JPanel();
        panel.setSize(size.x, size.y);
        panel.setBackground(color);
        return panel;

    }


    private void setPanel(JPanel panel1, JPanel panel2) {
        panel1.setVisible(false);
        add(panel2);
        panel2.setVisible(true);
        revalidate();
        repaint();
    }

    //添加面板
    private void addPanel(JPanel panel) {
        panels.add(panel);
        add(panel);
        setBounds(panel.getBounds());
    }
    public static void playMusic() {
        String pt = "D:/JAVA/game/";//文件地址前缀
        try {
            AudioInputStream audioInput = AudioSystem.getAudioInputStream(new File(pt + "BGM.wav"));//必须是wav格式
            Clip clip = AudioSystem.getClip();
            clip.open(audioInput);
            FloatControl gainControl = (FloatControl) clip.getControl(FloatControl.Type.MASTER_GAIN);
            gainControl.setValue(-20.0f);
            clip.start();
            clip.loop(Clip.LOOP_CONTINUOUSLY);//去掉就可以只播放一次，可以用作音效
        }catch (Exception e){
            e.printStackTrace();
        }
    }

}
class Tuple {
    int x;
    int y;

    public Tuple(int x, int y) {
        this.x = x;
        this.y = y;
    }
}

