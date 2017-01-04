# hello-world
rain's repository  
This Repository build in 2016.12.28 from rain.

1、typedef问题

```
//*****************************************************************************
//
// Special setup for access to a HAPI function.
//
//*****************************************************************************
typedef long (* volatile HAPI_CRC32_T)(unsigned char *, unsigned long);  //pointer to function函数指针
#define HAPI_CRC32_FUNC_PTR     0x00000048
#define P_HAPI_CRC32            ((HAPI_CRC32_T *)HAPI_CRC32_FUNC_PTR)
#define CalcCrc32(a,b)          (*P_HAPI_CRC32)(a,b)  

// Run the CRC calculation over the downloaded image, not including the CRC.
crcControl.crc[1] = CalcCrc32((uint8*)(HAL_OTA_DL_ADDR+PREAMBLE_OFFSET),crcControl.programSize-8);  

```   
13-16行代码解读：  
13行：给函数指针（指向函数的指针）起个别名，名字为HAPI_CRC32_T（类型别名）；指向函数(unsigned char * unsigned long )，函数带2个参数，返回值是long 

14-16行：封装CalcCrc32(a，b),函数指针指向0x00000048地址处，返回值为long型，具体值未知（没有对代码进行更深层次解析）

typedef用法参考链接：http://www.cnblogs.com/afarmer/archive/2011/05/05/2038201.html
