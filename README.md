# games

package games;

import java.awt.CardLayout;
import java.awt.Color;
import java.awt.Dimension;
import java.awt.Font;
import java.awt.FontFormatException;
import java.awt.Image;
import java.awt.Point;
import java.awt.Toolkit;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;
import java.util.LinkedList;
import javax.swing.ImageIcon;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JTextArea;
import javax.swing.JTextField;
import javax.swing.UIManager;

public class MainMenu implements ActionListener, Checker {
	JPanel GUI;
	JPanel panel, buttonpanel, helppanel, loadpanel ;
	JButton Play, Load, Help, Exit, Back, subname, shop, Game;
	Font font2 ;
	double Screenwidth, ScreenHeight;
	CardLayout cards = new CardLayout();
	LinkedList<Profile> profiles = new LinkedList<Profile>();
	JTextField name = new JTextField();
	JLabel error = new JLabel();
	String[] temp;
	Profile useprofile;
	JLabel name1 = new JLabel();

	public MainMenu() {
		// TODO Auto-generated constructor stub
	}

	public void CreateGUI() {
	
		Dimension screenSize = Toolkit.getDefaultToolkit().getScreenSize();
		Screenwidth = screenSize.getWidth();
		ScreenHeight = screenSize.getHeight();
		GUI = new JPanel();

		GUI.setLayout(null);

		GUI.setSize((int) Screenwidth, (int) ScreenHeight);
		GUI.setBackground(Color.WHITE);
		panel = new JPanel();

		panel.setLayout(cards);
		JLabel pic = new JLabel();

		ImageIcon maths1 = new ImageIcon(getClass().getClassLoader()
				.getResource("Pics/Gamesbox.png"));

		Image maths2 = maths1.getImage();

		maths2 = maths2.getScaledInstance((int) Screenwidth,
				(int) (ScreenHeight), 0);
		ImageIcon maths3 = new ImageIcon(maths2);
		pic.setSize((int) Screenwidth, (int) (ScreenHeight));

		pic.setIcon(maths3);
		pic.setVisible(true);
		pic.setLayout(null);

		float fontsize2 = (float) (Screenwidth / 60);
		try {
			font2 = Font.createFont(
					Font.TRUETYPE_FONT,
					getClass().getClassLoader()
							.getResourceAsStream("Font/FONT2.ttf")).deriveFont(
					fontsize2);
		} catch (FontFormatException | IOException e) {
			JOptionPane.showOptionDialog( null, e.getStackTrace(), null, 0, 0, null, null, null);
			e.printStackTrace();
	}
		panel.setSize((int) Screenwidth / 2, (int) ScreenHeight / 2);
		panel.setLocation((int) Screenwidth / 4, (int) ScreenHeight / 4);

		buttonpanel = new JPanel();
		buttonpanel = ButtonPanelcreate();

		try {
			UIManager
					.setLookAndFeel("com.sun.java.swing.plaf.nimbus.NimbusLookAndFeel");
		} catch (Exception e) {
			e.printStackTrace();
		}

		helppanel = new JPanel();
		helppanel = HelpPanelcreate();
		loadpanel = new JPanel();
		loadpanel = LoadPanelcreate();


		buttonpanel.setVisible(true);

		panel.add("w", buttonpanel);
		panel.add("e", helppanel);
		panel.add("r", loadpanel);
	
		
		GUI.add(panel);
		GUI.add(pic);

		GUI.setVisible(true);

	}

	public JPanel returnpanel() {
		return GUI;
	}

	public void show() {
		JFrame a = new JFrame();
		a.add(GUI);
		a.setVisible(true);
	}

	private int LocationLen(Dimension panel, Dimension comp, int pos) {
		int pointa = 0;
		pointa = (panel.height / 4) * pos;
		int pointb = 0;

		pointb = comp.height;

		return pointa - pointb / 2;

	}

	public int LocationWid(Dimension panel, Dimension comp, int pos) {

		int pointa = 0;
		pointa = (panel.width / 4) * pos;
		int pointb = 0;

		pointb = comp.width;

		return pointa - pointb / 2;

	}

	public JPanel CreatePanelcreate() {
		JPanel c = new JPanel();
		c.setLayout(null);
		c.setSize((int) Screenwidth / 2, (int) ScreenHeight / 2);
		c.setLocation((int) Screenwidth / 4, (int) ScreenHeight / 4);
		c.setBackground(Color.WHITE);

		name = new JTextField();
		name.setSize(panel.getSize().width / 2, panel.getSize().height / 8);
		name.setLocation(LocationWid(panel.getSize(), name.getSize(), 3),
				LocationLen(panel.getSize(), name.getSize(), 1));
		name.setVisible(true);
		name.setFont(font2);
		JLabel namelabel = new JLabel("Enter your name:");
		namelabel
				.setSize(panel.getSize().width / 3, panel.getSize().height / 8);
		namelabel.setLocation(LocationWid(panel.getSize(), name.getSize(), 1),
				LocationLen(panel.getSize(), name.getSize(), 1));
		namelabel.setFont(font2);
		subname = new JButton("Submit and Play!");
		subname.setSize((int) Screenwidth / 5, (int) ScreenHeight / 10);
		subname.setLocation(LocationWid(panel.getSize(), subname.getSize(), 1),
				LocationLen(panel.getSize(), subname.getSize(), 3));
		subname.setFont(font2);
		subname.addActionListener(this);
		error = new JLabel("");
		error.setFont(font2);
		error.setSize((int) (panel.getSize().width), panel.getSize().height / 3);
		error.setLocation(LocationWid(panel.getSize(), error.getSize(), 2),
				LocationLen(panel.getSize(), error.getSize(), 2));
		JButton back2 = new JButton("Back");
		back2.addActionListener(this);
		back2.setActionCommand("Back");
		back2.setSize(subname.getSize());
		back2.setLocation(LocationWid(panel.getSize(), back2.getSize(), 3),
				LocationLen(panel.getSize(), back2.getSize(), 3));
		back2.setFont(font2);

		if (profiles.size() > 3) {
			error.setText(("You already have 4 profiles, delete one to make another"));

			subname.setEnabled(false);
			name.setEditable(false);

		}
		c.add(back2);
		c.add(subname);
		c.add(error);
		c.add(namelabel);
		c.add(name);
		return c;
	}

	public JPanel HelpPanelcreate() {
		JPanel a = new JPanel();
		a.setLayout(null);
		a.setSize((int) Screenwidth / 2, (int) ScreenHeight / 2);
		a.setLocation((int) Screenwidth / 4, (int) ScreenHeight / 4);
		a.setBackground(Color.WHITE);
		JTextArea helptext = new JTextArea(
				"This programme will help you with your maths skills. \n Create a new profile to begin or load an exisiting one.\n If you try hard enough you might even unlock a surpise!");
		helptext.setFont(font2);
		helptext.setEditable(true);
		helptext.setWrapStyleWord(true);
		helptext.setVisible(true);
		helptext.setBorder(null);
		helptext.setLocation(0, 0);
		helptext.setSize(panel.getSize().width,
				(int) (panel.getSize().height * 0.6));
		JButton Back1 = new JButton("Back");

		Back1.setFont(font2);

		Back1.setSize(panel.getSize().width / 3,
				(int) (panel.getSize().height * 0.2));
		Back1.setLocation(LocationWid(a.getSize(), Back1.getSize(), 2),
				LocationLen(a.getSize(), Back1.getSize(), 3));

		Back1.addActionListener(this);
		Back1.setActionCommand("Back");
		Back1.setVisible(true);
		a.add(helptext);
		a.add(Back1);
		a.setVisible(true);
		return a;
	}


	public JPanel LoadPanelcreate() {
		// data();

		JPanel b = new JPanel();
		b.setLayout(null);

		b.setSize(panel.getSize());
		b.setLocation(0, 0);
		b.setBackground(Color.WHITE);
		Dimension pref = new Dimension(panel.getWidth() / 2,
				panel.getHeight() / 7);
		// if (!temp[0].equals("0")) {
		// for (int i = 0; i < temp.length; i++) {
		// System.out.println(i);
		// String temp2[] = temp[i].split(",");
		// Profile a = new Profile(temp2[0], temp2[1], temp2[2], temp2[3],
		// temp2[4], temp2[5], temp2[6]);
		// profiles.add(a);
		// JButton c = new JButton(a.getName());
		//
		// c.setActionCommand(Integer.toString(i + 1));
		// c.addActionListener(this);
		// c.setFont(font2);
		//
		// c.setSize(pref);
		// c.setLocation(loadpoint(i, c.getSize()));
		// b.add(c);
		// }
		//
		// }else{
		// JLabel nothing = new JLabel("No profiles found");
		// nothing.setFont(font2);
		// nothing.setSize(pref);
		// nothing.setLocation(loadpoint(2, nothing.getSize()));;
		// b.add(nothing);
		// }

		Back = new JButton("Back");

		Back.setFont(font2);

		Back.setHorizontalAlignment(0);
		Back.addActionListener(this);
		Back.setActionCommand("Back");
		Back.setVisible(true);

		Back.setSize(pref);
		Back.setLocation(loadpoint(4, Back.getSize()));

		b.add(Back);
		return b;
	}

	private Point loadpoint(int i, Dimension butt) {
		int spaceing = panel.getHeight() / 5;
		int mid = panel.getWidth() / 2;
		int x = mid - butt.width / 2;
		int y = spaceing * i;
		Point p = new Point(x, y);
		return p;
	}

	public JPanel ButtonPanelcreate() {
		try {
			UIManager
					.setLookAndFeel("com.sun.java.swing.plaf.nimbus.NimbusLookAndFeel");
		} catch (Exception e) {
			e.printStackTrace();
		}

		JPanel a = new JPanel();
		a.setLayout(null);
		a.setSize(panel.getSize());
		a.setLocation(0, 0);
		a.setBackground(Color.WHITE);
		Play = new JButton("Play!");
		Play.setFont(font2);

		Play.setSize((int) Screenwidth / 5, (int) ScreenHeight / 10);
		Play.setLocation(LocationWid(panel.getSize(), Play.getSize(), 2), 0);
		Play.addActionListener(this);

		Play.setActionCommand("Play");
		Play.setVisible(true);

		Exit = new JButton("Exit");
		Exit.setFont(font2);
		Exit.setSize((int) Screenwidth / 5, (int) ScreenHeight / 10);
		Exit.setLocation(LocationWid(panel.getSize(), Exit.getSize(), 3),
				LocationLen(panel.getSize(), Exit.getSize(), 3));
		Exit.addActionListener(this);
		Exit.setActionCommand("2");
		Exit.setVisible(true);

		Help = new JButton("Help");
		Help.setFont(font2);
		Help.setSize((int) Screenwidth / 5, (int) ScreenHeight / 10);
		Help.setLocation(LocationWid(panel.getSize(), Help.getSize(), 1),
				LocationLen(panel.getSize(), Help.getSize(), 3));
		Help.addActionListener(this);
		Help.setActionCommand("3");
		Help.setVisible(true);

		a.add(Play);

		a.add(Exit);
		a.add(Help);

		a.setVisible(true);
		return a;

	}

	public void actionPerformed(ActionEvent e) {
		System.out.println(e.getActionCommand());
		if (e.getSource().equals(Help)) {

			cards.show(panel, "e");
			GUI.revalidate();
			GUI.repaint();
		} else if (e.getActionCommand().equals("Back")) {
			cards.show(panel, "w");
			name1.setText("");
			GUI.revalidate();
			GUI.repaint();
		} else if (e.getSource().equals(Exit)) {
			MasterGUI.exit();
		
		
		} else if (e.getActionCommand().equals("Play")) {
			
			Gamesmenu gm = new Gamesmenu();
			gm.CreateGUI();
			MasterGUI.updateFrame(gm.returnpanel());


		} 

	}

	public Boolean Check() {
		if (name.getText().contains(":") || name.getText().contains(",")
				|| name.getText().isEmpty()) {
			error.setText("Do not use either : or , in your name!");
			name.setText("");
			GUI.repaint();
			GUI.revalidate();
			return false;
		} else {
			for (int f = 0; f < profiles.size(); f++) {
				if (name.getText().equals(profiles.get(f).getName())) {
					error.setText("Do not use either : or , in your name!");
					name.setText("");
					GUI.repaint();
					GUI.revalidate();
					return false;
				}
			}
		}
		return true;
	}
}
