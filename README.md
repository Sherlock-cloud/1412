import java.io.PrintWriter;
import java.net.Socket;
import java.util.ArrayList;

public class SocketManager extends ArrayList {
	synchronized void add(Socket socket){ //添加连接套接字方法
			super.add(socket);}
			synchronized void delete(Socket socket){//删除套接字方法
				super. remove(socket);}
				synchronized void sendClientConut(){ //输出当前聊天人数
					String info="当前聊天人数"+size();
					System.out. println(info);
					writeall(info);}//使用套接字输出流,输出信
					synchronized void writeall(String str){
					PrintWriter writer=null;
					Socket socket;
					for (int i=0;i<size();i++){//循环遍历套接字集合
								socket=(Socket)get(i);//获取指定套接字
						try{
						writer=new PrintWriter(socket.getOutputStream(),true);//创建输出流
						if(writer !=null)
							writer.println(str);

					} catch(Exception e){
							e.printStackTrace(); } }}}
							
							
							
							
							
							
							
							
							
				import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.net.ServerSocket;
import java.net.Socket;

public class ServerProcess{
		private SocketManager socketman=new SocketManager();
		void getserver(){
		try{
		ServerSocket serverSocket =new ServerSocket(7777);
		System.out.println("服务器套接字已创建");
		while(true){
		Socket socket=serverSocket.accept();//等待连接
		new write_Thread(socket).start();//启动线程
		socketman.add(socket);
		//调用添加套接字方法
		socketman.sendClientConut();}
		//将当前连接数输出
		} catch(Exception e){
		e.printStackTrace();}} 
		

	class write_Thread extends Thread{
//内部类
	Socket socket=null;//创建 Socket对象
	private BufferedReader reader;//	创建 Bufferedreader对象
	private PrintWriter writer;//创建Print Writer对象
	public write_Thread(Socket socket){//构造方法
		this.socket=socket; }
	public void run(){
		try {
			reader = new BufferedReader(
					new InputStreamReader(socket.getInputStream()));
			writer = new PrintWriter(
					socket.getOutputStream(), true);
			String msg;
			while ((msg=reader.readLine()) != null) {
				System.out.println(msg);
				socketman.writeall(msg);
			}
		}catch (Exception e){
			e.printStackTrace();
		}}}
		public static void main(String[]args){ //主方法
			ServerProcess server= new ServerProcess();//创建本类对象
			server.getServer();}

	private void getServer() {
	}
}


				
							

