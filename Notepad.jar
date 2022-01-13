import java.io.*;
import javax.swing.*;
import javax.swing.text.*;
import javax.swing.undo.*;
import java.awt.*;
import java.awt.event.*;
import javax.swing.filechooser.FileNameExtensionFilter;
import javax.swing.event.UndoableEditEvent;
import javax.swing.event.UndoableEditListener;

public class Notepad extends KeyAdapter implements ActionListener, KeyListener {

    int fsize = 20;
    private JTextArea area;
    private JScrollPane scpane;
    String text = "";

    JFrame f = new JFrame("AJP MICRO-20");
private Document editorPaneDocument;
protected UndoManager undoManager = new UndoManager();
    
    JTextField title;
    Font newFont;
    JPanel bottomPanel;
    JLabel detailsOfFile;
    JList fontFamilyList, fontStyleList, fontSizeList;
    JScrollPane sb;
    JMenuBar menuBar;
    JMenu file, edit, format;
    JMenuItem newdoc, open, save, print, exit, copy, paste, cut, selectall, fontfamily, fontstyle, fontsize, undo, redo;

    String fontFamilyValues[] = {"Agency FB", "Antiqua", "Architect", "Arial", "Calibri", "Comic Sans", "Courier", "Cursive", "Impact", "Serif", "Times New Roman"};
    String fontSizeValues[] = {"6", "11", "16", "21", "26", "31", "32", "41", "46", "47", "56", "61", "66", "71", "72", "80"};
    int[] stylevalue = {Font.PLAIN, Font.BOLD, Font.ITALIC};
    String[] fontStyleValues = {"PLAIN", "BOLD", "ITALIC"};
    String fontFamily, fontSize, fontStyle;
    int fstyle;
    int cl;
    int linecount;
    JScrollPane sp;

    public Notepad() {
        initUI();
        addActionEvents();
    }

   
        public void actionPerformed(ActionEvent ae) {
        if (ae.getActionCommand().equals("New")) {
            area.setText("");
        } 

        else if (ae.getActionCommand().equals("Open")) {
            JFileChooser chooser = new JFileChooser("C:/");
            chooser.setAcceptAllFileFilterUsed(false);
            FileNameExtensionFilter restrict = new FileNameExtensionFilter("Only .txt files", "txt");
            chooser.addChoosableFileFilter(restrict);

            int result = chooser.showOpenDialog(f);
            if (result == JFileChooser.APPROVE_OPTION) {
                File file = chooser.getSelectedFile();
                try {
                    FileReader reader = new FileReader(file);
                    BufferedReader br = new BufferedReader(reader);
                    area.read(br, null);
                    br.close();
                    area.requestFocus();
                    JOptionPane.showMessageDialog(null, "FILE OPENED SUCCESFULLY !!!!");
                } catch (Exception e) {
                    System.out.print(e);
                }
            }
        } 

        else if (ae.getActionCommand().equals("Save")) {
            final JFileChooser SaveAs = new JFileChooser();
            SaveAs.setApproveButtonText("Save");
            int actionDialog = SaveAs.showOpenDialog(f);
            if (actionDialog != JFileChooser.APPROVE_OPTION) {
                return;
            }
            File fileName = new File(SaveAs.getSelectedFile() + ".txt");
            BufferedWriter outFile = null;
            try {
                outFile = new BufferedWriter(new FileWriter(fileName));
                area.write(outFile);
                JOptionPane.showMessageDialog(null, "FILE SAVED SUCCESFULLY !!!!");
            } catch (IOException e) {
                e.printStackTrace();
            }
        }

        else if (ae.getActionCommand().equals("Print")) {
            try {
                area.print();
            } catch (Exception e) {
            }
        } 

        else if (ae.getActionCommand().equals("Exit")) {
            f.dispose();
        JOptionPane.showMessageDialog(null, "EXITED SUCCESFULLY !!!!" );
        } 

        else if (ae.getActionCommand().equals("Copy")) {
            text = area.getSelectedText();
            JOptionPane.showMessageDialog(null, "TEXT COPIED SUCCESFULLY !!!!");
        } 

        else if (ae.getActionCommand().equals("Paste")) {
            area.insert(text, area.getCaretPosition());
           JOptionPane.showMessageDialog(null, "TEXT PASTED SUCCESFULLY !!!!");
        } 

        else if (ae.getActionCommand().equals("Cut")) {
            text = area.getSelectedText();
            area.replaceRange("", area.getSelectionStart(), area.getSelectionEnd());

        } 

        else if (ae.getActionCommand().equals("Select All")) {
            area.selectAll();
        } 

        else if (ae.getActionCommand().equals("Fonts")) {
            JOptionPane.showConfirmDialog(null, fontFamilyList, "Choose Font Family", JOptionPane.OK_CANCEL_OPTION, JOptionPane.PLAIN_MESSAGE);
            fontFamily = String.valueOf(fontFamilyList.getSelectedValue());
            newFont = new Font(fontFamily, fstyle, fsize);
            area.setFont(newFont);
        } 

        else if (ae.getActionCommand().equals("Style")) {
            JOptionPane.showConfirmDialog(null, fontStyleList, "Choose Font Style", JOptionPane.OK_CANCEL_OPTION, JOptionPane.PLAIN_MESSAGE);
            fstyle = stylevalue[fontStyleList.getSelectedIndex()];
            newFont = new Font(fontFamily, fstyle, fsize);
            area.setFont(newFont);
        } 

        else if (ae.getActionCommand().equals("Size")) {
       
            JOptionPane.showConfirmDialog(null, fontSizeList, "Choose Font Size", JOptionPane.OK_CANCEL_OPTION, JOptionPane.PLAIN_MESSAGE);
            fontSize = String.valueOf(fontSizeList.getSelectedValue());
            fsize = Integer.parseInt(fontSize);
            newFont = new Font(fontFamily, fstyle, fsize);
            area.setFont(newFont);
        }
	else if(ae.getActionCommand().equals("Undo")){
		if(undoManager.canUndo()){
			undoManager.undo();
                 JOptionPane.showMessageDialog(null, "UNDO OPERATION IS SUCCESFULL !!!!");
		}
	}
	else if(ae.getActionCommand().equals("Redo")){
		if(undoManager.canRedo()){
			undoManager.redo();
                JOptionPane.showMessageDialog(null, "REDO OPTION IS SUCESSFULL !!!!");
		}
	}
    }

    @Override
    public void keyTyped(KeyEvent ke) {
        cl = area.getText().length();
        linecount = area.getLineCount();
        detailsOfFile.setText("Length: " + cl + " Line: " + linecount);
    }

    public void initUI() {
        detailsOfFile = new JLabel();     
        bottomPanel = new JPanel();
        menuBar = new JMenuBar();
        file = new JMenu("File");
        
        newdoc = new JMenuItem("New");
        newdoc.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_N, ActionEvent.CTRL_MASK));


        open = new JMenuItem("Open");
        open.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_O, ActionEvent.CTRL_MASK));


        save = new JMenuItem("Save");
        save.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_S, ActionEvent.CTRL_MASK));


        print = new JMenuItem("Print");     
        print.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_P, ActionEvent.CTRL_MASK));

       
        exit = new JMenuItem("Exit");
        exit.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_ESCAPE, 0));     
        

        edit = new JMenu("Edit");       
        copy = new JMenuItem("Copy");    
        copy.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_C, ActionEvent.CTRL_MASK));


        paste = new JMenuItem("Paste");     
        paste.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_V, ActionEvent.CTRL_MASK));
     

        cut = new JMenuItem("Cut");  
        cut.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_X, ActionEvent.CTRL_MASK));
 
    	
	undo = new JMenuItem("Undo");
	undo.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_Z, ActionEvent.CTRL_MASK));


	redo = new JMenuItem("Redo");
	redo.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_Y, ActionEvent.CTRL_MASK));


        selectall = new JMenuItem("Select All");    
        selectall.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_A, ActionEvent.CTRL_MASK));

        
        format = new JMenu("Format");
        fontfamily = new JMenuItem("Fonts");
        fontstyle = new JMenuItem("Style");  
        fontsize = new JMenuItem("Size");   
        fontFamilyList = new JList(fontFamilyValues);
        fontStyleList = new JList(fontStyleValues);
        fontSizeList = new JList(fontSizeValues);
        fontFamilyList.setSelectionMode(ListSelectionModel.SINGLE_SELECTION);
        fontStyleList.setSelectionMode(ListSelectionModel.SINGLE_SELECTION);
        fontSizeList.setSelectionMode(ListSelectionModel.SINGLE_SELECTION);

        area = new JTextArea();
        area.setFont(new Font("AERIAL", Font.PLAIN, 15));
        area.setLineWrap(true);
        area.setWrapStyleWord(true);
	area.getDocument().addUndoableEditListener(
		new UndoableEditListener(){
			public void undoableEditHappened(UndoableEditEvent e){
				undoManager.addEdit(e.getEdit());
			}
		}
	);
        scpane = new JScrollPane(area);
        scpane.setBorder(BorderFactory.createEmptyBorder());

        f.setJMenuBar(menuBar);

        menuBar.add(file);
        menuBar.add(edit);
        menuBar.add(format);

        file.add(newdoc);
        file.add(open);
        file.add(save);
        file.add(print);
        file.add(exit);

        edit.add(copy);
        edit.add(paste);
        edit.add(cut);
        edit.add(selectall);
	edit.add(undo);
	edit.add(redo);

        format.add(fontfamily);
        format.add(fontstyle);
        format.add(fontsize);

        bottomPanel.add(detailsOfFile);

        f.setBounds(0,0,1950,1050);
        f.setLayout(new BorderLayout());
        f.add(scpane, BorderLayout.CENTER);
        f.add(bottomPanel, BorderLayout.SOUTH);
        f.setVisible(true);
    }

public void addActionEvents() {
        newdoc.addActionListener(this);
        save.addActionListener(this);
        print.addActionListener(this);
        exit.addActionListener(this);
        copy.addActionListener(this);
        paste.addActionListener(this);
        cut.addActionListener(this);
        selectall.addActionListener(this);
        open.addActionListener(this);
        fontfamily.addActionListener(this);
        fontsize.addActionListener(this);
        fontstyle.addActionListener(this);
	undo.addActionListener(this);
	redo.addActionListener(this);
    }
        
        public static void main(String ar[]) {
        Notepad np = new Notepad();
    }
}