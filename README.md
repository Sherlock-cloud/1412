import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.net.Socket;

public class Client extends JFrame implements Runnable{
		private JPanel jpanel =new JPanel();
		private JLabel namelabel=new JLabel("姓名:");//标签对象
        private JTextField namefield=new JTextField();//文框对象
private JTextArea msgarea =new JTextArea();//文本域对象
private JTextField sendfield=new JTextField();
private JScrollPane jscrollpanel =new javax.swing.JScrollPane();
private BufferedReader reader;//创建 Bufferedreader类对象
private PrintWriter writer;
private Socket socket;//创建套接字对象
public Client(String title) {
	super(title);
	this.setSize(360, 340);
	this.add(jpanel);
	jpanel.setLayout(null);
	msgarea.setEditable(false);//msg Area对象为不可编译状态
	jpanel.add(namelabel);//将标签添加到面板上
	namelabel.setBounds(10, 10, 60, 20);//设置布局
	jpanel.add(namefield);
	namefield.setBounds(60, 10, 270, 21);
	jpanel.add(sendfield);
	sendfield.setBounds(10, 270, 320, 21);
	msgarea.setColumns(20);
	msgarea.setRows(5);
	jscrollpanel.setViewportView(msgarea);
	jpanel.add(jscrollpanel);
	jscrollpanel.setBounds(10, 40, 320, 220);
	sendfield.addActionListener(new ActionListener(){
		@Override
		public void actionPerformed (ActionEvent e){
			writer.println(namefield.getText() + ":" + sendfield.getText());//将用户名、用户输入信息写入流中
			sendfield.setText("");
		}
	});
}//将发送文本框中的内容清空
public void run(){
	while(true){
		try{ //在文本域中将读取内容分行显示
			msgarea. append(reader.readLine()+"\n");
		} catch(Exception e){
			e.printStackTrace();}}}
			void getSocket(){//创建套接字方法
			msgarea.append("尝试与服务器连接");
			try {
				socket = new Socket("127.0.0.1", 7777);
				msgarea.append("聊天准备完毕");//文本域中的信息
				reader = new BufferedReader(
						new InputStreamReader(socket.getInputStream()));
				writer = new PrintWriter(
						socket.getOutputStream(), true);
				new Thread(this).start();//启动线程
			}catch(Exception e){
				e.printStackTrace();}}
				public static void main(String[]args){
					Client client=new Client("迷你聊天屋");
							client. setVisible(true);}}
