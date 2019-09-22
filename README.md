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
