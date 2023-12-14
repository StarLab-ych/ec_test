

# 基础用法

前提：7个节点，运行节点client（IP：192.168.7.101），6个存储节点datanode（IP：192.168.7.102到107），client和datanode节点间可以免密ssh登录root用户

1.  ssh 192.168.7.101 -l root //ssh登录client

2. tar xzvf ych_ec_test.tar.gz  && cd ych_ec_test  //解压并进入

3. cmake . && make  //编译

4. cd script/      //进入脚本文件夹

5.   ./mkdir_save_directory.sh 102 107 //创建datanode节点保存文件夹（仅第一次）

     ./rm_save_directory.sh 102 107     //删除保存文件夹

6. ./scp_datanode.sh 102 107   //发送执行文件datanode到datanode

7. ./start_all_datanode.sh 102 107  //执行102到107的datanode

   ./kill_all_datanode.sh 102 107  //杀死102到107的datanode

   ./kill_ip_datanode.sh 102// //杀死单个节点102

8. ./start_client.sh -w src_10MB.mp4 dst_10MB.mp4   //写

   ./start_client.sh -r read_10MB.mp4 dst_10MB.mp4  //读

9. vim ../include/ych_ec_test.h  //自定义修改

10. cmake . && make  //程序修改编译

11. GDB //gdb调试运行

# 代码结构

.
├── CMakeLists.txt
├── include
│   ├── galois.h
│   ├── jerasure.h
│   ├── reed_sol.h
│   └── ych_ec_test.h
├── log
│   └── datanode_log.out
├── RADEME.md
├── script
│   ├── kill_all_datanode.sh
│   ├── kill_datanode.sh
│   ├── kill_ip_datanode.sh
│   ├── mkdir_save_directory.sh
│   ├── rm_save_directory.sh
│   ├── scp_datanode.sh
│   ├── start_all_datanode.sh
│   ├── start_client.sh
│   └── start_datanode.sh
├── src
│   ├── client
│   │   └── client_main.cpp
│   ├── datanode
│   │   └── datanode_main.cpp
│   └── erasure_coding
│       ├── galois.cpp
│       ├── jerasure.cpp
│       └── reed_sol.cpp
└── test_file
    ├── file_size
    ├── read
    └── write
        └── src_10MB.mp4

11 directories, 23 files