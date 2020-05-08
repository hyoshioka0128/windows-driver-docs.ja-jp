---
title: 動詞を HD オーディオ コーデックとやり取りする
description: 動詞を HD オーディオ コーデックとやり取りする
ms.assetid: d93013fa-5b09-4616-bc71-5d3838337717
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 724d4265ae5a4b63d1b8ffb22566bb265fefdbd0
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925606"
---
# <a name="communicating-verbs-with-the-hd-audio-codec"></a>動詞を HD オーディオ コーデックとやり取りする


IOCTL\_azyour abus\_sendverbs ioctl は、オーディオアダプターのサウンドトポロジを定義するときに、hdau の pin 構成ツールによって使用されます。 他の目的では、この IOCTL を使用しないでください。 IOCTL\_az氏 abus\_sendverbs に関するこの情報は、設計と実装のみを文書化するために提供されています。 この IOCTL は、Windows 7 Hdaudio クラスドライバーでサポートされています。

High definition (HD) オーディオコーデックは、動詞の受信と応答を行うことができます。 これらの動詞とコーデックの応答は、 [HD オーディオ仕様](https://www.intel.com/content/www/us/en/products/docs/chipsets/high-definition-audio.html)の一部として記載されています。

Windows 7 以降のバージョンの Windows オペレーティングシステムでは、HD audio クラスドライバーは IOCTL\_azの\_sendverbs ioctl を使用して、オーディオコーデックと動詞をやり取りします。 IOCTL\_az氏 abus\_sendverbs は、次の例に示すように定義されています。

```cpp
#define IOCTL_AZALIABUS_SENDVERBS CTL_CODE(FILE_DEVICE_UNKNOWN, 1, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

ファイル\_\_デバイスの不明、\_メソッドのバッファー、およびファイル\_\_へのアクセスの詳細については、Windows SDK の Devioctl ヘッダーファイルを参照してください。

オーディオコーデックとの通信を開始するために、クラスドライバーは、次のパラメーターを使用して[DeviceIoControl](https://docs.microsoft.com/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol)関数を呼び出します。

```cpp
BOOL DeviceIoControl(
  (HANDLE) hDevice,                      // handle to device
  IOCTL_AZALIABUS_SENDVERBS,             // dwIoControlCode
  NULL,                                  // lpInBuffer
  0,                                     // nInBufferSize
  (LPVOID) lpOutBuffer,                  // output buffer
  (DWORD) nOutBufferSize,                // size of output buffer
  (LPDWORD) lpBytesReturned,             // number of bytes returned
  (LPOVERLAPPED) lpOverlapped            // OVERLAPPED structure
);
```

[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)の呼び出しが成功した場合、0以外の値が返されます。 呼び出しが失敗した場合、または待機状態になっている (直ちに処理されない) 場合、 **DeviceIoControl**は0の値を返します。 クラスドライバーは、より詳細なエラーメッセージを表示するために、 [GetLastError](https://docs.microsoft.com/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror)を呼び出すことができます。

オーディオドライバーで pin 構成の既定値を変更する必要がある\_場合は、IOCTL\_azの abus sendverbs を使用して、設定されたオーディオコーデックの動詞を送受信できます。 オーディオコーデックとの通信が pin 構成に関するものではない場合、オーディオコーデックは Get 動詞にのみ応答します。

次の例は、AzCorbeEntry 構造体とハンドルをパラメーターとして受け取り、コーデックから Azcorbeentry を返す関数を示しています。

```cpp
AzRirbEntry SendVerb(HANDLE handle, AzCorbEntry verb)
{
  UserModeCodecCommandPacket c;
  UserModeCodecResponsePacket r;
  c.NumCommands = 1;
  c.Command[0] = verb;
  DWORD BytesReturned;

//A nonzero value is returned for a successful call and it is interpreted as TRUE  
BOOL rc = DeviceIoControl(handle, IOCTL_AZALIABUS_SENDVERBS, &c, sizeof(c), &r, sizeof(r), &BytesReturned, 0);

  if(!rc)
  {
    printf("Failed to communicate with the device!\n");
    return 0;
  }

  if(BytesReturned != sizeof(r))
  {
    printf("Wrong number of bytes returned!\n");
    return 0;
  }

  return r.Response[0];
}
```

前のコード例で使用されているデータ型と構造体は、次の例で定義されています。

### <a name="span-idazcorbentryspanspan-idazcorbentryspan-azcorbentry"></a><span id="azcorbentry"></span><span id="AZCORBENTRY"></span>AzCorbEntry

```cpp
struct AzCorbEntry
{
  ULONG Verb        : 20; // 0:19
  ULONG NodeId      : 7;  // 20:26
  ULONG IndirectNID : 1;  // 27
  ULONG LinkId      : 4;  // 28:31
  enum {Invalid = 0xffffffff};
  AzCorbEntry(ULONG x = 0)
  :
    Verb(x),
    NodeId(x >> 20),
    IndirectNID(x >> 27),
    LinkId(x >> 28) {}
  operator ULONG()
  {
    return Verb | NodeId << 20 | IndirectNID << 27 | LinkId << 28;
  }
};
```

### <a name="span-idazrirbentryspanspan-idazrirbentryspan-azrirbentry"></a><span id="azrirbentry"></span><span id="AZRIRBENTRY"></span>AzRirbEntry

```cpp
struct AzRirbEntry
{
  union
  {
    struct 
    {
      ULONG Response  : 21; // 0 : 20
      ULONG SubTag    : 5; // 21 : 25
      ULONG Tag       : 6; // 26 : 31
    } UnsolicitedForm;

    ULONG Response    : 32; // 0:31
  };
  ULONG Sdi         : 4;  // 32:35
  ULONG Unsolicited : 1;  // 36
  ULONG Reserved0   : 26; // 37:62
  ULONG Valid       : 1;  // 63 note this bit only exists
                          // on the "link". The fact that the response
                          // got into memory assures that it is valid
  AzRirbEntry (ULONGLONG x = 0)
  {
    Response = x & 0xffffffff;
    Sdi = x >> 32;
    Unsolicited = x >> 36;
    Reserved0 = x >> 37;
    Valid = x >> 63;
  }
  operator ULONGLONG()
  {
    return (ULONGLONG)Response | (ULONGLONG)Sdi << 32 | (ULONGLONG)Unsolicited << 36 | (ULONGLONG)Reserved0 << 37 | (ULONGLONG)Valid << 63;
  }
};
```

次の2つの構造体を動詞転送 IOCTL と共に使用して、オーディオドライバーと HD オーディオコーデック間でコマンドおよび応答の転送を有効にします。

### <a name="span-idusermodecodeccommandpacketspanspan-idusermodecodeccommandpacketspan-usermodecodeccommandpacket"></a><span id="usermodecodeccommandpacket"></span><span id="USERMODECODECCOMMANDPACKET"></span>UserModeCodecCommandPacket

```cpp
typedef struct _UserModeCodecCommandPacket
{
  ULONG NumCommands;      // number of commands in this packet
  AzCorbEntry Command[1]; // variable length array of verbs
} UserModeCodecCommandPacket;
```

### <a name="span-idusermodecodecresponsepacketspanspan-idusermodecodecresponsepacketspan-usermodecodecresponsepacket"></a><span id="usermodecodecresponsepacket"></span><span id="USERMODECODECRESPONSEPACKET"></span>UserModeCodecResponsePacket

```cpp
typedef struct _UserModeCodecResponsePacket
{
  ULONG NumResponses;       // on successful IOCTL, this will be updated with the number of responses.
  AzRirbEntry Response[1];  // Variable length array of responses. lpOutBuffer param to DeviceIoControl
                            // must point to sufficient space to hold this IOCTL with all its responses 
} UserModeCodecResponsePacket;
```

 

 




