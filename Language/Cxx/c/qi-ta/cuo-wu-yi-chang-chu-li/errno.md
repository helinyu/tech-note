---
description: 错误类型的集合
---

# errno

```
#ifndef _SYS_ERRNO_H_
#define _SYS_ERRNO_H_

#include <sys/cdefs.h>


#if defined(__STDC_WANT_LIB_EXT1__) && __STDC_WANT_LIB_EXT1__ >= 1
#include <sys/_types/_errno_t.h>
#endif

__BEGIN_DECLS
extern int * __error(void);
#define errno (*__error())
__END_DECLS

/*
 * Error codes
 */

#define EPERM           1               /* Operation not permitted */
#define ENOENT          2               /* No such file or directory */
#define ESRCH           3               /* No such process */
#define EINTR           4               /* Interrupted system call */
#define EIO             5               /* Input/output error */
#define ENXIO           6               /* Device not configured */
#define E2BIG           7               /* Argument list too long */
#define ENOEXEC         8               /* Exec format error */
#define EBADF           9               /* Bad file descriptor */
#define ECHILD          10              /* No child processes */
#define EDEADLK         11              /* Resource deadlock avoided */
                                        /* 11 was EAGAIN */
#define ENOMEM          12              /* Cannot allocate memory */
#define EACCES          13              /* Permission denied */
#define EFAULT          14              /* Bad address */
#if __DARWIN_C_LEVEL >= __DARWIN_C_FULL
#define ENOTBLK         15              /* Block device required */
#endif
#define EBUSY           16              /* Device / Resource busy */
#define EEXIST          17              /* File exists */
#define EXDEV           18              /* Cross-device link */
#define ENODEV          19              /* Operation not supported by device */
#define ENOTDIR         20              /* Not a directory */
#define EISDIR          21              /* Is a directory */
#define EINVAL          22              /* Invalid argument */
#define ENFILE          23              /* Too many open files in system */
#define EMFILE          24              /* Too many open files */
#define ENOTTY          25              /* Inappropriate ioctl for device */
#define ETXTBSY         26              /* Text file busy */
#define EFBIG           27              /* File too large */
#define ENOSPC          28              /* No space left on device */
#define ESPIPE          29              /* Illegal seek */
#define EROFS           30              /* Read-only file system */
#define EMLINK          31              /* Too many links */
#define EPIPE           32              /* Broken pipe */

/* math software */
#define EDOM            33              /* Numerical argument out of domain */
#define ERANGE          34              /* Result too large */

/* non-blocking and interrupt i/o */
#define EAGAIN          35              /* Resource temporarily unavailable */
#define EWOULDBLOCK     EAGAIN          /* Operation would block */
#define EINPROGRESS     36              /* Operation now in progress */
#define EALREADY        37              /* Operation already in progress */

/* ipc/network software -- argument errors */
#define ENOTSOCK        38              /* Socket operation on non-socket */
#define EDESTADDRREQ    39              /* Destination address required */
#define EMSGSIZE        40              /* Message too long */
#define EPROTOTYPE      41              /* Protocol wrong type for socket */
#define ENOPROTOOPT     42              /* Protocol not available */
#define EPROTONOSUPPORT 43              /* Protocol not supported */
#if __DARWIN_C_LEVEL >= __DARWIN_C_FULL
#define ESOCKTNOSUPPORT 44              /* Socket type not supported */
#endif
#define ENOTSUP         45              /* Operation not supported */
#if !__DARWIN_UNIX03 && !defined(KERNEL)
/*
 * This is the same for binary and source copmpatability, unless compiling
 * the kernel itself, or compiling __DARWIN_UNIX03; if compiling for the
 * kernel, the correct value will be returned.  If compiling non-POSIX
 * source, the kernel return value will be converted by a stub in libc, and
 * if compiling source with __DARWIN_UNIX03, the conversion in libc is not
 * done, and the caller gets the expected (discrete) value.
 */
#define EOPNOTSUPP       ENOTSUP        /* Operation not supported on socket */
#endif /* !__DARWIN_UNIX03 && !KERNEL */

#if __DARWIN_C_LEVEL >= __DARWIN_C_FULL
#define EPFNOSUPPORT    46              /* Protocol family not supported */
#endif
#define EAFNOSUPPORT    47              /* Address family not supported by protocol family */
#define EADDRINUSE      48              /* Address already in use */
#define EADDRNOTAVAIL   49              /* Can't assign requested address */

/* ipc/network software -- operational errors */
#define ENETDOWN        50              /* Network is down */
#define ENETUNREACH     51              /* Network is unreachable */
#define ENETRESET       52              /* Network dropped connection on reset */
#define ECONNABORTED    53              /* Software caused connection abort */
#define ECONNRESET      54              /* Connection reset by peer */
#define ENOBUFS         55              /* No buffer space available */
#define EISCONN         56              /* Socket is already connected */
#define ENOTCONN        57              /* Socket is not connected */
#if __DARWIN_C_LEVEL >= __DARWIN_C_FULL
#define ESHUTDOWN       58              /* Can't send after socket shutdown */
#define ETOOMANYREFS    59              /* Too many references: can't splice */
#endif
#define ETIMEDOUT       60              /* Operation timed out */
#define ECONNREFUSED    61              /* Connection refused */

#define ELOOP           62              /* Too many levels of symbolic links */
#define ENAMETOOLONG    63              /* File name too long */

/* should be rearranged */
#if __DARWIN_C_LEVEL >= __DARWIN_C_FULL
#define EHOSTDOWN       64              /* Host is down */
#endif
#define EHOSTUNREACH    65              /* No route to host */
#define ENOTEMPTY       66              /* Directory not empty */

/* quotas & mush */
#if __DARWIN_C_LEVEL >= __DARWIN_C_FULL
#define EPROCLIM        67              /* Too many processes */
#define EUSERS          68              /* Too many users */
#endif
#define EDQUOT          69              /* Disc quota exceeded */

/* Network File System */
#define ESTALE          70              /* Stale NFS file handle */
#if __DARWIN_C_LEVEL >= __DARWIN_C_FULL
#define EREMOTE         71              /* Too many levels of remote in path */
#define EBADRPC         72              /* RPC struct is bad */
#define ERPCMISMATCH    73              /* RPC version wrong */
#define EPROGUNAVAIL    74              /* RPC prog. not avail */
#define EPROGMISMATCH   75              /* Program version wrong */
#define EPROCUNAVAIL    76              /* Bad procedure for program */
#endif

#define ENOLCK          77              /* No locks available */
#define ENOSYS          78              /* Function not implemented */

#if __DARWIN_C_LEVEL >= __DARWIN_C_FULL
#define EFTYPE          79              /* Inappropriate file type or format */
#define EAUTH           80              /* Authentication error */
#define ENEEDAUTH       81              /* Need authenticator */

/* Intelligent device errors */
#define EPWROFF         82      /* Device power is off */
#define EDEVERR         83      /* Device error, e.g. paper out */
#endif

#define EOVERFLOW       84              /* Value too large to be stored in data type */

/* Program loading errors */
#if __DARWIN_C_LEVEL >= __DARWIN_C_FULL
#define EBADEXEC        85      /* Bad executable */
#define EBADARCH        86      /* Bad CPU type in executable */
#define ESHLIBVERS      87      /* Shared library version mismatch */
#define EBADMACHO       88      /* Malformed Macho file */
#endif

#define ECANCELED       89              /* Operation canceled */

#define EIDRM           90              /* Identifier removed */
#define ENOMSG          91              /* No message of desired type */
#define EILSEQ          92              /* Illegal byte sequence */
#if __DARWIN_C_LEVEL >= __DARWIN_C_FULL
#define ENOATTR         93              /* Attribute not found */
#endif

#define EBADMSG         94              /* Bad message */
#define EMULTIHOP       95              /* Reserved */
#define ENODATA         96              /* No message available on STREAM */
#define ENOLINK         97              /* Reserved */
#define ENOSR           98              /* No STREAM resources */
#define ENOSTR          99              /* Not a STREAM */
#define EPROTO          100             /* Protocol error */
#define ETIME           101             /* STREAM ioctl timeout */

#if __DARWIN_UNIX03 || defined(KERNEL)
/* This value is only discrete when compiling __DARWIN_UNIX03, or KERNEL */
#define EOPNOTSUPP      102             /* Operation not supported on socket */
#endif /* __DARWIN_UNIX03 || KERNEL */

#define ENOPOLICY       103             /* No such policy registered */

#if __DARWIN_C_LEVEL >= 200809L
#define ENOTRECOVERABLE 104             /* State not recoverable */
#define EOWNERDEAD      105             /* Previous owner died */
#endif

#if __DARWIN_C_LEVEL >= __DARWIN_C_FULL
#define EQFULL          106             /* Interface output queue is full */
#define ELAST           106             /* Must be equal largest errno */
#endif

#endif /* _SYS_ERRNO_H_ */


```



翻译成为中文\
以下是`errno`错误类型的中文翻译：

1. **EPERM**：操作不被允许。
2. **ENOENT**：没有这样的文件或目录。
3. **ESRCH**：没有这样的进程。
4. **EINTR**：系统调用被中断。
5. **EIO**：输入/输出错误。
6. **ENXIO**：设备未配置。
7. **E2BIG**：参数列表过长。
8. **ENOEXEC**：执行格式错误。
9. **EBADF**：无效的文件描述符。
10. **ECHILD**：没有子进程。
11. **EDEADLK**：资源死锁避免。
12. **ENOMEM**：无法分配内存。
13. **EACCES**：权限被拒绝。
14. **EFAULT**：错误的地址。
15. **ENOTBLK**：需要块设备。
16. **EBUSY**：设备/资源忙。
17. **EEXIST**：文件已存在。
18. **EXDEV**：跨设备链接。
19. **ENODEV**：设备不支持该操作。
20. **ENOTDIR**：不是目录。
21. **EISDIR**：是目录。
22. **EINVAL**：无效参数。
23. **ENFILE**：系统中打开的文件过多。
24. **EMFILE**：打开的文件过多。
25. **ENOTTY**：对设备的无效ioctl。
26. **ETXTBSY**：文本文件忙。
27. **EFBIG**：文件过大。
28. **ENOSPC**：设备上没有足够的空间。
29. **ESPIPE**：非法寻址。
30. **EROFS**：只读文件系统。
31. **EMLINK**：链接过多。
32. **EPIPE**：管道破裂。
33. **EDOM**：数值参数超出范围。
34. **ERANGE**：结果过大。
35. **EAGAIN**：资源暂时不可用。
36. **EWOULDBLOCK**：操作会阻塞。
37. **EINPROGRESS**：操作正在进行。
38. **EALREADY**：操作已经在进行中。
39. **ENOTSOCK**：在非套接字上进行套接字操作。
40. **EDESTADDRREQ**：需要目标地址。
41. **EMSGSIZE**：消息过长。
42. **EPROTOTYPE**：套接字的协议类型错误。
43. **ENOPROTOOPT**：协议不可用。
44. **EPROTONOSUPPORT**：协议不支持。
45. **ESOCKTNOSUPPORT**：套接字类型不支持。
46. **ENOTSUP**：不支持该操作。
47. **EOPNOTSUPP**：在套接字上不支持的操作。
48. **EPFNOSUPPORT**：协议族不支持。
49. **EAFNOSUPPORT**：协议族不支持的地址族。
50. **EADDRINUSE**：地址已在使用中。
51. **EADDRNOTAVAIL**：无法分配请求的地址。
52. **ENETDOWN**：网络关闭。
53. **ENETUNREACH**：网络不可达。
54. **ENETRESET**：网络重置连接。
55. **ECONNABORTED**：软件导致连接中止。
56. **ECONNRESET**：连接被对方重置。
57. **ENOBUFS**：没有可用的缓冲区空间。
58. **EISCONN**：套接字已经连接。
59. **ENOTCONN**：套接字未连接。
60. **ESHUTDOWN**：套接字关闭后无法发送。
61. **ETOOMANYREFS**：引用过多，无法拆分。
62. **ETIMEDOUT**：操作超时。
63. **ECONNREFUSED**：连接被拒绝。
64. **ELOOP**：符号链接层次过多。
65. **ENAMETOOLONG**：文件名过长。
66. **EHOSTDOWN**：主机关闭。
67. **EHOSTUNREACH**：无法到达主机。
68. **ENOTEMPTY**：目录非空。
69. **EPROCLIM**：进程过多。
70. **EUSERS**：用户过多。
71. **EDQUOT**：磁盘配额超出。
72. **ESTALE**：过期的NFS文件句柄。
73. **EREMOTE**：路径中远程层次过多。
74. **EBADRPC**：RPC结构错误。
75. **ERPCMISMATCH**：RPC版本错误。
76. **EPROGUNAVAIL**：RPC程序不可用。
77. **EPROGMISMATCH**：程序版本错误。
78. **EPROCUNAVAIL**：程序的错误过程。
79. **ENOLCK**：没有可用的锁。
80. **ENOSYS**：功能未实现。
81. **EFTYPE**：不适当的文件类型或格式。
82. **EAUTH**：认证错误。
83. **ENEEDAUTH**：需要身份验证器。
84. **EPWROFF**：设备电源关闭。
85. **EDEVERR**：设备错误，例如纸张用尽。
86. **EOVERFLOW**：值过大无法存储。
87. **EBADEXEC**：坏可执行文件。
88. **EBADARCH**：可执行文件中的坏CPU类型。
89. **ESHLIBVERS**：共享库版本不匹配。
90. **EBADMACHO**：Macho文件格式错误。
91. **ECANCELED**：操作已被取消。
92. **EIDRM**：标识符已被删除。
93. **ENOMSG**：没有所需类型的消息。
94. **EILSEQ**：非法字节序列。
95. **ENOATTR**：找不到属性。
96. **EBADMSG**：坏消息。
97. **EMULTIHOP**：保留。
98. **ENODATA**：流中没有可用的消息。
99. **ENOLINK**：保留。
100. **ENOSR**：没有流资源。
101. **ENOSTR**：不是流。
102. **EPROTO**：协议错误。
103. **ETIME**：流ioctl超时。
104. **EOPNOTSUPP**：在套接字上不支持的操作。
105. **ENOPOLICY**：没有注册此类策略。
106. **ENOTRECOVERABLE**：状态不可恢复。
107. **EOWNERDEAD**：前任所有者已死亡。
108. **EQFULL**：接口输出队列已满。
109. **ELAST**：必须等于最大的errno值。

如果你需要对某个具体错误代码进行深入的探讨，请告诉我！

