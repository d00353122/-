非阻塞式I/O包括非阻塞输入操作，非阻塞输出操作，非阻塞接收外来连接，非阻塞发起外出连接。
包括的函数有：read, readv, recv, recvfrom, recvmsg, write, writev, send, sendto, sendmsg, accept;

1、创建socket的时候，指定socket是异步的，在type的参数中设置SOCK_NONBLOCK标志即可；
	int socket(int domain, int type, int protocol);
	int s = socket(AF_INET, SOCK_STREAM | SOCK_NONBLOCK, IPPROTO_TCP);

2、使用fcntl函数：
	fcntl(sockfd, F_SETFL, fcntl(sockfd, F_GETFL, 0) | O_NONBLOCK); //设置非阻塞
	fcntl(sockfd, F_SETFL, fcntl(sockfd, F_GETFL, 0) & ~ O_NONBLOCK); //设置非阻塞

3、使用ioctl函数
	ioctl(sockfd, FIONBIO, 1);  //1:非阻塞 0:阻塞
