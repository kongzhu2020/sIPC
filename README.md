# sIPC
## WHAT
基于socket的轻量级跨进程通信框架

## WHY
**特点**
+ 轻量级嵌入式系统IPC方案
+ 5G友好的socket基础框架
+ 依赖少好移植

**功能**
+ 基于protobuf的远程过程（RPC）机制 (无感的函数调用方式)
+ 基于epoll的事件分发机制（用于线程调度）
+ 基于匿名共享内存的circlebuffer机制 （用于类似视频流的传输）

## HOW
### **跨进程方案对比**

方案|内存拷贝|数据传输|通信结构
--|:--:|--:|--:
binder|一次|parcel|C/S结构
socket|两次|parcel|全双工
ashmem|零次|parcel|全双工

### **iIPC接口设计方案**
- 远程过程调用
```
iIPCServerManager
{
    + singleton instance;

    + int registerIPC(int name, int pid, int ppid);
    + int unregisterIPC(int name);

    - init();
    - destroy();
}
```

- 事件分发机制
- 匿名共享内存机制