# 目录

<!--自动插入TOC：https://github.com/ekalinin/github-markdown-toc-->
<!--ts-->
   * [目录](#目录)
   * [基本知识](#基本知识)
      * [TCHAR](#tchar)

<!-- Added by: luyl, at: 2018-11-21T14:49+08:00 -->

<!--te-->

----

# Windows编程-基本知识

## TCHAR

C++支持两种字符集，如下：

```
ANSI字符集：Multi-Byte Character
Unicode字符集：Unicode Character
```

微软为了统一这两套编码，所以有了TCHAR，通过条件编译(_UNICODE宏和UNICODE宏)控制实际使用的字符集。

```
typedef char CHAR
typedef wchar_t WCHAR

typedef CHAR * PCHAR, * LPCH, * PCH, * NPSTR, * LPSTR, * PSTR;
typedef CONST CHAR * LPCCH, * PCCH, * LPCSTR, * PCSTR;

typedef WCHAR * PWCHAR, * LPWCH, * PWCH, * NWPSTR, * LPWSTR, * PWSTR;
typedef CONST WCHAR * LPCWCH, * PCWCH, * LPCWSTR, * PCWSTR;

#ifdef UNICODE
typedef WCHAR TCHAR, * PTCHAR;
typedef LPWSTR LPTCH, PTCH, PTSTR, LPTSTR;
typedef LPCWSTR LPCTSTR;
#define __TEXT(quote) L##quote
#else
typedef char TCHAR, * PTCHAR;
typedef LPSTR LPTCH, PTCH, PTSTR, LPTSTR;
typedef LPCSTR LPCTSTR;
#define __TEXT(quote) quote
#endif

#define TEXT(quote) __TEXT(quote)

```

TCHAR类型在Multi-Byte字符集下占1个字节，在Unicode字符集下占2个字节。同一个TCAHR类型的数组变量在不同字符集下，长度是不同的。

```
TCHAR ptszArray[10];
在Unicode字符集下，长度为20个字节
在Multi-Byte字符集下，长度为10个字节
```

----

# Office

## Excel

### 基本函数