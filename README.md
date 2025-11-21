import java.awt.EventQueue;
import java.awt.Font;

import javax.swing.JFrame;
import javax.swing.JPanel;
import javax.swing.border.EmptyBorder;
import net.miginfocom.swing.MigLayout;
import javax.swing.JLabel;
import javax.swing.JTextField;
import java.awt.Color;
import javax.swing.border.LineBorder;
import javax.swing.table.DefaultTableModel;
import javax.swing.JScrollPane;
import java.awt.event.KeyAdapter;
import java.awt.event.KeyEvent;
import javax.swing.JTable;
import javax.swing.SwingConstants;
import javax.swing.border.CompoundBorder;
import javax.swing.UIManager;


public class kzennethgui extends JFrame {

	private static final long serialVersionUID = 1L;
	private JPanel contentPane;
	private JTextField txtBarcode;
	private JTextField txtItem;
	private JTextField txtPrice;
	private JTextField txtQty;
	private JTable table;

	/**
	 * Launch the application.
	 */
	public static void main(String[] args) {
		EventQueue.invokeLater(new Runnable() {
			public void run() {
				try {
					kzennethgui frame = new kzennethgui();
					frame.setVisible(true);
				} catch (Exception e) {
					e.printStackTrace();
				}
			}
		});
	}

	/**
	 * Create the frame.
	 */
	
	public kzennethgui() {
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setBounds(100, 100, 573, 369);
		contentPane = new JPanel();
		contentPane.setBackground(new Color(115, 153, 157));
		contentPane.setBorder(new EmptyBorder(5, 5, 5, 5));
		setContentPane(contentPane);
		contentPane.setLayout(null);
		
		
		
		JPanel panel = new JPanel();
		panel.setBorder(new LineBorder(new Color(0, 255, 255), 2, true));
		panel.setBackground(new Color(128, 255, 255));
		panel.setBounds(339, 144, 208, 119);
		contentPane.add(panel);
		panel.setLayout(new MigLayout("", "[][][][grow]", "[][][][]"));
		
		DefaultTableModel model = new DefaultTableModel();
		model.addColumn("ITEM");
		model.addColumn("PRICE");
		model.addColumn("QTY");
		model.addColumn("SUBTOTAL");
		
		JLabel lblBarcode = new JLabel("BARCODE");
		panel.add(lblBarcode, "cell 0 0");
		
		txtBarcode = new JTextField();
		txtBarcode.addKeyListener(new KeyAdapter() {
			@Override
			public void keyPressed(KeyEvent e) {
				if(e.getKeyCode() == KeyEvent.VK_ENTER) {
					posData posD = new posData();
					int barcode = Integer.parseInt(txtBarcode.getText());
					posD.searchItem(barcode);
					txtItem.setText(posD.getItem());
					txtPrice.setText(""+posD.getPrice());
					txtQty.requestFocus();
				}
			}
		});
		panel.add(txtBarcode, "cell 2 0,alignx center");
		txtBarcode.setColumns(10);
		
		JLabel lblItem = new JLabel("ITEM");
		panel.add(lblItem, "cell 0 1");
		
		txtItem = new JTextField();
		txtItem.setEditable(false);
		panel.add(txtItem, "cell 2 1,growx");
		txtItem.setColumns(10);
		
		JLabel lblPrice = new JLabel("PRICE");
		panel.add(lblPrice, "cell 0 2");
		
		JLabel lblGrandTotal = new JLabel("");
		lblGrandTotal.setHorizontalAlignment(SwingConstants.RIGHT);
		lblGrandTotal.setForeground(new Color(255, 0, 0));
		lblGrandTotal.setFont(new Font("Tahoma", Font.BOLD, 16));
		lblGrandTotal.setBackground(new Color(255, 255, 255));
		lblGrandTotal.setBounds(339, 94, 208, 40);
		contentPane.add(lblGrandTotal);
		
		txtPrice = new JTextField();
		txtPrice.setEditable(false);
		panel.add(txtPrice, "cell 2 2,growx");
		txtPrice.setColumns(10);
		
		JLabel lblQty = new JLabel("QUANTITY");
		panel.add(lblQty, "cell 0 3");
		
		txtQty = new JTextField();
		txtQty.addKeyListener(new KeyAdapter() {
			@Override
			public void keyPressed(KeyEvent e) {
				if(e.getKeyCode() == KeyEvent.VK_ENTER) {
					
					float price = Float.parseFloat(txtPrice.getText());
					float qty = Float.parseFloat(txtQty.getText());
					//float Input = qty;
					//is_float_only = qty.isfloat();
					float SubTotal = qty * price;
					float grandTotal =+ SubTotal;
					lblGrandTotal.setText(""+grandTotal);
					
					model.addRow(new Object[] {
						txtItem.getText(),
						txtPrice.getText(),
						txtQty.getText(),
						SubTotal
					});
					ClearFields();
					}
			}
		});
		panel.add(txtQty, "cell 2 3,growx");
		txtQty.setColumns(10);
		
		JPanel panel_1 = new JPanel();
		panel_1.setBorder(new LineBorder(new Color(64, 128, 128), 2, true));
		panel_1.setBackground(new Color(128, 255, 255));
		panel_1.setBounds(10, 94, 319, 213);
		contentPane.add(panel_1);
		panel_1.setLayout(null);
		
		table = new JTable(model);
		table.setBorder(new EmptyBorder(2, 1, 2, 1));
		table.setForeground(new Color(255, 0, 0));
		table.setBackground(new Color(103, 84, 89));
		table.setFont(new Font("Tahoma", Font.BOLD, 10));
		JScrollPane scrollPane = new JScrollPane(table);
		scrollPane.setBounds(10, 11, 299, 191);
		panel_1.add(scrollPane);
		
		JLabel lblDeveloper = new JLabel("Developer: Kenneth Pilaspilas");
		lblDeveloper.setBounds(0, 318, 208, 14);
		contentPane.add(lblDeveloper);
		

	}
	
	public void ClearFields() {
		txtBarcode.setText("");
		txtItem.setText("");
		txtPrice.setText("");
		txtQty.setText("");
		txtBarcode.requestFocus();
	}
}
