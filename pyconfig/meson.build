
is_darwin = (host_machine.system() == 'darwin')
is_linux = (host_machine.system() == 'linux')

chflags_run = cc.run('''
  #include <sys/stat.h>
  #include <unistd.h>
  int main(int argc, char *argv[])
  {
    if(chflags(argv[0], 0) != 0)
      return 1;
    return 0;
  }''')

lchflags_run = cc.run('''
  #include <sys/stat.h>
  #include <unistd.h>
  int main(int argc, char *argv[])
  {
    if(lchflags(argv[0], 0) != 0)
      return 1;
    return 0;
  }''')

# true on mac?
broken_sem_getvalue_run = cc.run('''
  #include <unistd.h>
  #include <fcntl.h>
  #include <stdio.h>
  #include <semaphore.h>
  #include <sys/stat.h>

  int main(void){
    sem_t *a = sem_open("/autocftw", O_CREAT, S_IRUSR|S_IWUSR, 0);
    int count;
    int res;
    if(a==SEM_FAILED){
      perror("sem_open");
      return 1;

    }
    res = sem_getvalue(a, &count);
    sem_close(a);
    sem_unlink("/autocftw");
    return res==-1 ? 1 : 0;
  }''')

pyconfig_data = configuration_data({
  'ALIGNOF_LONG': cc.alignment('long'),
  'ALIGNOF_MAX_ALIGN_T':cc.alignment('max_align_t'),
  'ALIGNOF_SIZE_T': cc.alignment('size_t'),
  'DOUBLE_IS_LITTLE_ENDIAN_IEEE754': true,
  'ENABLE_IPV6': true,
  'HACL_CAN_COMPILE_SIMD128': cc.has_multi_arguments('-msse', '-msse2', '-msse3', '-msse4.1', '-msse4.2'),
  'HACL_CAN_COMPILE_SIMD256': cc.has_argument('-mavx2'),
  'HAVE_ACCEPT': true,
  'HAVE_ACOSH': true,
  'HAVE_ADDRINFO': true,
  'HAVE_ASINH': true,
  'HAVE_ATANH': true,
  'HAVE_BIND': true,
  'HAVE_BROKEN_SEM_GETVALUE': (broken_sem_getvalue_run.compiled() and broken_sem_getvalue_run.returncode() != 0).to_int(),
  'HAVE_BUILTIN_ATOMIC': true,
  'HAVE_CHFLAGS': chflags_run.compiled() and chflags_run.returncode() == 0,
  'HAVE_CLOCK_GETRES': true,
  'HAVE_CLOCK_GETTIME': true,
  'HAVE_CLOCK_NANOSLEEP': cc.has_function('clock_nanosleep', prefix: '#include <time.h>'),
  'HAVE_CLOCK_SETTIME': true,
  'HAVE_CLOCK_T': true,
  'HAVE_COMPUTED_GOTOS': true,
  'HAVE_CONNECT': true,
  # 'HAVE_COPY_FILE_RANGE': true, #fixme
  'HAVE_CTERMID_R': cc.has_function('ctermid_r', prefix: '#include <stdio.h>'),
  'HAVE_CURSES_FILTER': true,
  'HAVE_CURSES_HAS_KEY': true,
  'HAVE_CURSES_IMMEDOK': true,
  'HAVE_CURSES_IS_PAD': true,
  'HAVE_CURSES_IS_TERM_RESIZED': true,
  'HAVE_CURSES_RESIZETERM': true,
  'HAVE_CURSES_RESIZE_TERM': true,
  'HAVE_CURSES_SYNCOK': true,
  'HAVE_CURSES_TYPEAHEAD': true,
  'HAVE_CURSES_USE_ENV': true,
  'HAVE_CURSES_WCHGAT': true,
  'HAVE_DECL_RTLD_DEEPBIND': cc.has_define('RTLD_DEEPBIND', prefix: '#include <dlfcn.h>').to_int(),
  'HAVE_DECL_RTLD_GLOBAL': cc.has_define('RTLD_GLOBAL', prefix: '#include <dlfcn.h>').to_int(),
  'HAVE_DECL_RTLD_LAZY': cc.has_define('RTLD_LAZY', prefix: '#include <dlfcn.h>').to_int(),
  'HAVE_DECL_RTLD_LOCAL': cc.has_define('RTLD_LOCAL', prefix: '#include <dlfcn.h>').to_int(),
  'HAVE_DECL_RTLD_MEMBER': cc.has_define('RTLD_MEMBER', prefix: '#include <dlfcn.h>').to_int(),
  'HAVE_DECL_RTLD_NODELETE': cc.has_define('RTLD_NODELETE', prefix: '#include <dlfcn.h>').to_int(),
  'HAVE_DECL_RTLD_NOLOAD': cc.has_define('RTLD_NOLOAD', prefix: '#include <dlfcn.h>').to_int(),
  'HAVE_DECL_RTLD_NOW': cc.has_define('RTLD_NOW', prefix: '#include <dlfcn.h>').to_int(),
  'HAVE_DEVICE_MACROS': true,
  'HAVE_DEV_PTMX': true,
  'HAVE_DIRENT_D_TYPE': true,
  'HAVE_DIRFD': true,
  'HAVE_DLOPEN': true,
  'HAVE_DUP2': true,
  # 'HAVE_DUP3': true,
  'HAVE_DYLD_SHARED_CACHE_CONTAINS_PATH': is_darwin, # fixme: cc.has_define('_dyld_shared_cache_contains_path', prefix: '#include <mach-o/dyld.h>'),
  'HAVE_DYNAMIC_LOADING': true,
  'HAVE_EPOLL': cc.has_function('epoll', prefix: '#include <sys/epoll.h>'),
  'HAVE_EPOLL_CREATE1': cc.has_function('epoll_create1', prefix: '#include <sys/epoll.h>'),
  'HAVE_ERF': true,
  'HAVE_ERFC': true,
  'HAVE_EVENTFD': cc.has_function('eventfd', prefix: '#include <sys/eventfd.h>'),
  'HAVE_EXPM1': true,
  'HAVE_FCHDIR': true,
  'HAVE_FFI_CLOSURE_ALLOC': 1,
  'HAVE_FFI_PREP_CIF_VAR': 1,
  'HAVE_FFI_PREP_CLOSURE_LOC': 1,
  'HAVE_FLOCK': true,
  'HAVE_FORKPTY': true,
  'HAVE_FSEEKO': true,
  'HAVE_FSTATVFS': true,
  'HAVE_FSYNC': true,
  'HAVE_FTELLO': true,
  'HAVE_GCC_ASM_FOR_X64': true, #fixme
  'HAVE_GCC_ASM_FOR_X87': true, #fixme
  'HAVE_GCC_UINT128_T': true,
  'HAVE_GETADDRINFO': true,
  'HAVE_GETC_UNLOCKED': true,
  'HAVE_GETENTROPY': true,
  'HAVE_GETGROUPS': true,
  'HAVE_GETHOSTBYADDR': true,
  'HAVE_GETHOSTBYNAME': true,
  'HAVE_GETHOSTBYNAME_R': true, #fixme
  'HAVE_GETHOSTBYNAME_R_6_ARG': true, #fixme
  'HAVE_GETNAMEINFO': true,
  'HAVE_GETPROTOBYNAME': true,
  'HAVE_GETRANDOM': cc.has_function('getrandom', prefix: '#include <sys/random.h>'),
  'HAVE_GETRANDOM_SYSCALL': false, # true on linux, but why would I want it to be used?
  # 'HAVE_GETRESGID': true, #fixme
  # 'HAVE_GETRESUID': true, #fixme
  'HAVE_GETSERVBYNAME': true,
  'HAVE_GETSERVBYPORT': true,
  'HAVE_GETSOCKNAME': true,
  'HAVE_HSTRERROR': true,
  'HAVE_HTOLE64': true, #fixme
  'HAVE_INET_ATON': true,
  'HAVE_INET_NTOA': true,
  'HAVE_INET_PTON': true,
  'HAVE_KQUEUE': cc.has_function('kqueue', prefix: ['#include <sys/types.h>', '#include <sys/event.h>']),
  'HAVE_LCHFLAGS': lchflags_run.compiled() and lchflags_run.returncode() == 0,
  'HAVE_LCHMOD': not is_linux,
  'HAVE_LIBDB': cc.has_header('ndbm.h'),
  'HAVE_LIBDL': true,
  'HAVE_LIBSQLITE3': true,
  'HAVE_LINK': true,
  'HAVE_LINUX_CAN_RAW_FD_FRAMES': is_linux, #fixme
  'HAVE_LINUX_CAN_RAW_JOIN_FILTERS': is_linux, #fixme
  'HAVE_LISTEN': true,
  'HAVE_LOG1P': true,
  'HAVE_LOG2': true,
  'HAVE_LOGIN_TTY': true,
  'HAVE_LONG_DOUBLE': true,
  'HAVE_MAKEDEV': true,
  # 'HAVE_MEMFD_CREATE': true, #fixme
  # 'HAVE_MREMAP': true, #fixme
  'HAVE_NANOSLEEP': true,
  'HAVE_NCURSESW': true,
  'HAVE_OPENPTY': true,
  'HAVE_PANELW': true, #fixme
  # 'HAVE_PRLIMIT': true, #fixme
  'HAVE_PROTOTYPES': true,
  'HAVE_PTHREAD_GETCPUCLOCKID': true,
  'HAVE_PTHREAD_SIGMASK': true,
  # 'HAVE_PTSNAME_R': true, #fixme
  # 'HAVE_PWRITEV2': true, #fixme
  'HAVE_RECVFROM': true,
  'HAVE_RL_APPEND_HISTORY': true, #fixme
  'HAVE_RL_CATCH_SIGNAL': true, #fixme
  'HAVE_RL_COMPDISP_FUNC_T': true, #fixme
  'HAVE_RL_COMPLETION_APPEND_CHARACTER': true,
  'HAVE_RL_COMPLETION_DISPLAY_MATCHES_HOOK': true,
  'HAVE_RL_COMPLETION_MATCHES': true,
  'HAVE_RL_COMPLETION_SUPPRESS_APPEND': true, #fixme
  'HAVE_RL_PRE_INPUT_HOOK': true,
  'HAVE_RL_RESIZE_TERMINAL': true, #fixme
  'HAVE_SENDTO': true,
  'HAVE_SETGROUPS': true,
  # 'HAVE_SETNS': true, #fixme
  # 'HAVE_SETRESGID': true, #fixme
  # 'HAVE_SETRESUID': true, #fixme
  'HAVE_SETSOCKOPT': true,
  'HAVE_SHM_OPEN': true,
  'HAVE_SHM_UNLINK': true,
  'HAVE_SIGINFO_T_SI_BAND': true,
  'HAVE_SOCKADDR_ALG': cc.has_type('sockaddr_alg', prefix: '#include <linux/if_alg.h>'),
  'HAVE_SOCKADDR_SA_LEN': cc.has_member('struct sockaddr', 'sa_len', prefix: '#include <sys/socket.h>'),
  'HAVE_SOCKADDR_STORAGE': true,
  'HAVE_SOCKET': true,
  'HAVE_SOCKETPAIR': true,
  'HAVE_SOCKLEN_T': true,
  # 'HAVE_SPLICE': true, #fixme
  'HAVE_SSIZE_T': 1,
  'HAVE_STATVFS': true,
  'HAVE_STAT_TV_NSEC': cc.has_member('struct stat', 'st_atim', prefix: '#include <sys/stat.h>'),
  'HAVE_STAT_TV_NSEC2': cc.has_member('struct stat', 'st_atimespec', prefix: '#include <sys/stat.h>'),
  'HAVE_STD_ATOMIC': true,
  'HAVE_STRUCT_PASSWD_PW_GECOS': true,
  'HAVE_STRUCT_PASSWD_PW_PASSWD': true,
  'HAVE_STRUCT_STAT_ST_BIRTHTIME': cc.has_member('struct stat', 'st_birthtime', prefix: '#include <sys/stat.h>'),
  'HAVE_STRUCT_STAT_ST_BLKSIZE': cc.has_member('struct stat', 'st_blksize', prefix: '#include <sys/stat.h>'),
  'HAVE_STRUCT_STAT_ST_BLOCKS': cc.has_member('struct stat', 'st_blocks', prefix: '#include <sys/stat.h>'),
  'HAVE_STRUCT_STAT_ST_FLAGS': cc.has_member('struct stat', 'st_flags', prefix: '#include <sys/stat.h>'),
  'HAVE_STRUCT_STAT_ST_GEN': cc.has_member('struct stat', 'st_gen', prefix: '#include <sys/stat.h>'),
  'HAVE_STRUCT_STAT_ST_RDEV': cc.has_member('struct stat', 'st_rdev', prefix: '#include <sys/stat.h>'),
  'HAVE_STRUCT_TM_TM_ZONE': true,
  'HAVE_SYMLINK': true,
  'HAVE_SYSTEM': true,
  'HAVE_TIMERFD_CREATE': cc.has_function('timerfd_create', prefix: '#include <sys/timerfd.h>'),
  'HAVE_TM_ZONE': true,
  # 'HAVE_UNSHARE': true, #fixme
  'HAVE_UUID_GENERATE_TIME_SAFE': true, #fixme
  'HAVE_WORKING_TZSET': true,
  'HAVE_ZLIB_COPY': zlib_dep.found(),
  'HAVE___UINT128_T': true,
  'MAJOR_IN_MKDEV': false,
  'MAJOR_IN_SYSMACROS': false, #fixme
  'MVWDELCH_IS_EXPRESSION': true,
  'PTHREAD_KEY_T_IS_COMPATIBLE_WITH_INT': true, #fixme
  'PTHREAD_SYSTEM_SCHED_SUPPORTED': true,
  'PYTHREAD_NAME_MAXLEN': 15, #fixme
  'PY_BUILTIN_HASHLIB_HASHES': '"md5,sha1,sha2,sha3,blake2"',
  'PY_COERCE_C_LOCALE': true,
  'PY_HAVE_PERF_TRAMPOLINE': with_perf_trampoline,
  'PY_SQLITE_HAVE_SERIALIZE': true,
  'PY_SSL_DEFAULT_CIPHERS': true,
  'PY_SUPPORT_TIER': true,
  'Py_FFI_SUPPORT_C_COMPLEX': true,
  'Py_HAVE_C_COMPLEX': true,
  'Py_NORMALIZE_CENTURY': true, #fixme
  'Py_RL_STARTUP_HOOK_TAKES_ARGS': true, #fixme mac
  'Py_STRFTIME_C99_SUPPORT': true,
  'RETSIGTYPE': 'void',
  'SIZEOF_DOUBLE': cc.sizeof('double'),
  'SIZEOF_FLOAT': cc.sizeof('float'),
  'SIZEOF_FPOS_T': cc.sizeof('fpos_t'),
  'SIZEOF_INT': cc.sizeof('int'),
  'SIZEOF_LONG': cc.sizeof('long'),
  'SIZEOF_LONG_DOUBLE': cc.sizeof('long double'),
  'SIZEOF_LONG_LONG': cc.sizeof('long long'),
  'SIZEOF_OFF_T': cc.sizeof('off_t', prefix: '#include <sys/types.h>'),
  'SIZEOF_PID_T': cc.sizeof('pid_t', prefix: '#include <sys/types.h>'),
  'SIZEOF_PTHREAD_KEY_T': cc.sizeof('pthread_key_t', prefix: '#include <pthread.h>'),
  'SIZEOF_PTHREAD_T': cc.sizeof('pthread_t', prefix: '#include <pthread.h>'),
  'SIZEOF_SHORT': cc.sizeof('short'),
  'SIZEOF_SIZE_T': cc.sizeof('size_t'),
  'SIZEOF_TIME_T': cc.sizeof('time_t', prefix: '#include <time.h>'),
  'SIZEOF_UINTPTR_T': cc.sizeof('uintptr_t', prefix: '#include <stdint.h>'),
  'SIZEOF_VOID_P': cc.sizeof('void*'),
  'SIZEOF_WCHAR_T': cc.sizeof('wchar_t'),
  'SIZEOF__BOOL': cc.sizeof('_Bool'),
  'STDC_HEADERS': true,
  'SYS_SELECT_WITH_SYS_TIME': true,
  'THREAD_STACK_SIZE': '0x1000000', #fixme mac
  'WINDOW_HAS_FLAGS': true, #fixme mac
  'WITH_DECIMAL_CONTEXTVAR': true,
  'WITH_DOC_STRINGS': true,
  'WITH_DYLD': is_darwin,
  'WITH_MIMALLOC': true,
  'WITH_PYMALLOC': 1,
  '_DARWIN_C_SOURCE': true,
  '_FILE_OFFSET_BITS': 64,
  '_LARGEFILE_SOURCE': true,
  '_NETBSD_SOURCE': true,
  '_POSIX_C_SOURCE': '200809L', #fixme
  '_PYTHONFRAMEWORK': '""',
  '_REENTRANT': true,
  # '_XOPEN_SOURCE': 700, #fixme
  '_XOPEN_SOURCE_EXTENDED': true, #fixme
  '__BSD_VISIBLE': true,

  'AC_APPLE_UNIVERSAL_BUILD': false,
  'AIX_BUILDDATE': false,
  'AIX_GENUINE_CPLUSPLUS': false,
  'ALT_SOABI': false,
  'ANDROID_API_LEVEL': false,
  'DOUBLE_IS_ARM_MIXED_ENDIAN_IEEE754': false,
  'DOUBLE_IS_BIG_ENDIAN_IEEE754': false,
  'GETPGRP_HAVE_ARG': false,
  'HAVE_ALIGNED_REQUIRED': false,
  'HAVE_ALTZONE': false,
  'HAVE_BROKEN_MBSTOWCS': false,
  'HAVE_BROKEN_NICE': false,
  'HAVE_BROKEN_PIPE_BUF': false,
  'HAVE_BROKEN_POLL': false,
  'HAVE_BROKEN_POSIX_SEMAPHORES': false,
  'HAVE_BROKEN_PTHREAD_SIGMASK': false,
  'HAVE_BROKEN_UNSETENV': false,
  'HAVE_DECL_TZNAME': false,
  'HAVE_DEV_PTC': false,
  'HAVE_FSEEK64': false,
  'HAVE_FTELL64': false,
  'HAVE_GCC_ASM_FOR_MC68881': false,
  'HAVE_GETHOSTBYNAME_R_3_ARG': false,
  'HAVE_GETHOSTBYNAME_R_5_ARG': false,
  'HAVE_GLIBC_MEMMOVE_BUG': false,
  'HAVE_IPA_PURE_CONST_BUG': false,
  'HAVE_LARGEFILE_SUPPORT': false,
  'HAVE_LIBDLD': false,
  'HAVE_LIBIEEE': false,
  'HAVE_LIBSENDFILE': false,
  'HAVE_NCURSES': false,
  'HAVE_NON_UNICODE_WCHAR_T_REPRESENTATION': false,
  'HAVE_PANEL': false,
  'HAVE_PTHREAD_DESTRUCTOR': false,
  'HAVE_PTHREAD_STUBS': false,
  'HAVE_TZNAME': false,
  'HAVE_USABLE_WCHAR_T': false,
  'HAVE_UUID_CREATE': false,
  'HAVE_UUID_ENC_BE': false,
  'PACKAGE_BUGREPORT': false,
  'PACKAGE_NAME': false,
  'PACKAGE_STRING': false,
  'PACKAGE_TARNAME': false,
  'PACKAGE_URL': false,
  'PACKAGE_VERSION': false,
  'POSIX_SEMAPHORES_NOT_ENABLED': false,
  'PYLONG_BITS_IN_DIGIT': false,
  'PY_SQLITE_ENABLE_LOAD_EXTENSION': false,
  'PY_SSL_DEFAULT_CIPHER_STRING': false,
  'Py_DEBUG': false,
  'Py_ENABLE_SHARED': false,
  'Py_GIL_DISABLED': false,
  'Py_HASH_ALGORITHM': false,
  'Py_STATS': false,
  'Py_SUNOS_VERSION': false,
  'Py_TRACE_REFS': false,
  'SETPGRP_HAVE_ARG': false,
  'SIGNED_RIGHT_SHIFT_ZERO_FILLS': false,
  'TIMEMODULE_LIB': false,
  'TM_IN_SYS_TIME': false,
  'USE_COMPUTED_GOTOS': false,
  'WITH_DTRACE': false,
  'WITH_EDITLINE': false,
  'WITH_LIBINTL': false,
  'WITH_NEXT_FRAMEWORK': false,
  'WITH_VALGRIND': false,
  'X87_DOUBLE_ROUNDING': false,
  '_BSD_SOURCE': false,
  '_INCLUDE__STDC_A1_SOURCE': false,
  '_LARGE_FILES': false,
  '_POSIX_THREADS': false,
  '_WASI_EMULATED_GETPID': false,
  '_WASI_EMULATED_PROCESS_CLOCKS': false,
  '_WASI_EMULATED_SIGNAL': false,
})

# copied as-is from configure.ac
check_headers_str = '''
  alloca.h asm/types.h bluetooth.h conio.h direct.h dirent.h dlfcn.h endian.h errno.h fcntl.h grp.h
  io.h langinfo.h libintl.h libutil.h linux/auxvec.h sys/auxv.h linux/can/raw.h linux/fs.h linux/limits.h linux/memfd.h
  linux/netfilter_ipv4.h linux/random.h linux/soundcard.h
  linux/tipc.h linux/wait.h netdb.h net/ethernet.h net/if.h netinet/in.h netpacket/packet.h poll.h process.h pthread.h pty.h
  sched.h setjmp.h shadow.h signal.h spawn.h stropts.h sys/audioio.h sys/bsdtty.h sys/devpoll.h
  sys/endian.h sys/epoll.h sys/event.h sys/eventfd.h sys/file.h sys/ioctl.h sys/kern_control.h
  sys/loadavg.h sys/lock.h sys/memfd.h sys/mkdev.h sys/mman.h sys/modem.h sys/param.h sys/pidfd.h sys/poll.h
  sys/random.h sys/resource.h sys/select.h sys/sendfile.h sys/socket.h sys/soundcard.h sys/stat.h
  sys/statvfs.h sys/sys_domain.h sys/syscall.h sys/sysmacros.h sys/termio.h sys/time.h sys/times.h sys/timerfd.h
  sys/types.h sys/uio.h sys/un.h sys/utsname.h sys/wait.h sys/xattr.h sysexits.h syslog.h
  termios.h util.h utime.h utmp.h wchar.h
'''
check_headers = check_headers_str.replace('  ', ' ').replace('\n', '').split(' ')

foreach h : check_headers
  def_name = h.underscorify().to_upper()
  pyconfig_data.set(f'HAVE_@def_name@', cc.has_header(h))
endforeach

check_functions_str = '''
  accept4 alarm bind_textdomain_codeset chmod chown clock closefrom close_range confstr
  copy_file_range ctermid dup dup3 execv explicit_bzero explicit_memset
  faccessat fchmod fchmodat fchown fchownat fdopendir fdwalk fexecve
  fork fork1 fpathconf fstatat ftime ftruncate futimens futimes futimesat
  gai_strerror getegid geteuid getgid getgrent getgrgid getgrgid_r
  getgrnam_r getgrouplist gethostname getitimer getloadavg getlogin
  getpeername getpgid getpid getppid getpriority _getpty
  getpwent getpwnam_r getpwuid getpwuid_r getresgid getresuid getrusage getsid getspent
  getspnam getuid getwd grantpt if_nameindex initgroups kill killpg lchown linkat
  lockf lstat lutimes madvise mbrtowc memrchr mkdirat mkfifo mkfifoat
  mknod mknodat mktime mmap mremap nice openat opendir pathconf pause pipe
  pipe2 plock poll posix_fadvise posix_fallocate posix_openpt posix_spawn posix_spawnp
  posix_spawn_file_actions_addclosefrom_np
  pread preadv preadv2 process_vm_readv
  pthread_cond_timedwait_relative_np pthread_condattr_setclock pthread_init
  pthread_kill pthread_getname_np pthread_setname_np
  ptsname ptsname_r pwrite pwritev pwritev2 readlink readlinkat readv realpath renameat
  rtpSpawn sched_get_priority_max sched_rr_get_interval sched_setaffinity
  sched_setparam sched_setscheduler sem_clockwait sem_getvalue sem_open
  sem_timedwait sem_unlink sendfile setegid seteuid setgid sethostname
  setitimer setlocale setpgid setpgrp setpriority setregid setresgid
  setresuid setreuid setsid setuid setvbuf shutdown sigaction sigaltstack
  sigfillset siginterrupt sigpending sigrelse sigtimedwait sigwait
  sigwaitinfo snprintf splice strftime strlcpy strsignal symlinkat sync
  sysconf tcgetpgrp tcsetpgrp tempnam timegm times tmpfile
  tmpnam tmpnam_r truncate ttyname umask uname unlinkat unlockpt utimensat utimes vfork
  wait wait3 wait4 waitid waitpid wcscoll wcsftime wcsxfrm wmemcmp writev
  getpagesize pthread_getcpuclockid chroot fdatasync
'''
check_functions = check_functions_str.replace('  ', ' ').replace('\n', '').split(' ')

int_tests = [
  'sem_getvalue',
  'sem_open',
  'sem_unlink',
  'mkdirat',
]
foreach f : check_functions
  def_name = f.underscorify().to_upper()
  prefix = [
    '#include <fcntl.h>',
    '#include <sched.h>',
    '#include <semaphore.h>',
    '#include <stdio.h>',
    '#include <sys/socket.h>',
    '#include <sys/stat.h>',
    '#include <sys/time.h>',
    '#include <sys/wait.h>',
    '#include <unistd.h>',
    '#include <sys/uio.h>',
    '#include <string.h>',
    '#include <sys/utsname.h>',
    '#include <signal.h>',
    '#include <time.h>',
    '#include <pthread.h>',
    '#include <pwd.h>',
    '#if __has_include(<libintl.h>)',
    '  #include <libintl.h>',
    '#endif',
  ]
  val = cc.has_function(f, prefix: prefix)
  val = (f in int_tests ? val.to_int() : val)
  if pyconfig_data.has(f'HAVE_@def_name@')
    message(f'replace HAVE_@def_name@')
  endif
  pyconfig_data.set(f'HAVE_@def_name@', val)
endforeach

#linux specific hacks
if is_linux
  pyconfig_data.set('HAVE_TIMEGM', true)
endif

#macos scpecific hacks
if is_darwin
  pyconfig_data.set('HAVE_GETPAGESIZE', false)
  pyconfig_data.set('HAVE_CHROOT', false) #temporary, fixme
  pyconfig_data.set('HAVE_SENDFILE', false) #temporary, fixme
endif

# undefined because found in headers, what it is it supposed to be defined to remains unknown

# clock_t
# const
# gid_t
# mode_t
# off_t
# pid_t
# signed
# size_t
# socklen_t
# uid_t