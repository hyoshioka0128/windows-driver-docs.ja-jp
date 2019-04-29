---
title: 動詞を HD オーディオ コーデックとやり取りする
description: 動詞を HD オーディオ コーデックとやり取りする
ms.assetid: d93013fa-5b09-4616-bc71-5d3838337717
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71f8ec7ff40cd04a6236fef85a75b933365a78b8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333877"
---
# <a name="communicating-verbs-with-the-hd-audio-codec"></a>動詞を HD オーディオ コーデックとやり取りする


IOCTL\_AZALIABUS\_オーディオ アダプターのサウンドのトポロジを定義するときに、SENDVERBS IOCTL が Hdau.exe 暗証番号 (pin) の構成ツールによって使用されます。 他の目的は、この IOCTL を使用しないでください。 この IOCTL について\_AZALIABUS\_SENDVERBS がドキュメントの設計と実装だけに提供されます。 この IOCTL は、Windows 7 Hdaudio.sys オーディオ クラス ドライバーでサポートされます。

高精細 (HD) オーディオ コーデックでは、動詞に応答を受信できます。 これらの動詞とこれらの動詞をコーデックの応答がの一部として記載されている[、HD オーディオ仕様](https://go.microsoft.com/fwlink/p/?linkid=169394)します。

Windows 7 および Windows オペレーティング システムの以降のバージョンでは、HD オーディオ クラス ドライバーは、IOCTL を使用して\_AZALIABUS\_SENDVERBS IOCTL 動詞オーディオ コーデックとの通信にします。 IOCTL\_AZALIABUS\_SENDVERBS は次の例に示すように定義されます。

```cpp
#define IOCTL_AZALIABUS_SENDVERBS CTL_CODE(FILE_DEVICE_UNKNOWN, 1, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

ファイルの詳細については\_デバイス\_不明、メソッド\_バッファーに格納された、およびファイル\_ANY\_アクセス、Windows SDK の Devioctl.h ヘッダー ファイルを参照してください。

クラス ドライバーが呼び出しオーディオ コーデックとの通信を開始するのには、 [DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=124239)関数は次のパラメーター。

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

場合に呼び出し[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)が成功すると、0 以外の値はすべて返します。 呼び出しが故障したかが保留されています (処理されませんすぐに)、 **DeviceIoControl**ゼロ値を返します。 クラスのドライバーを呼び出すことができます[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)より詳細なエラー メッセージ。

IOCTL を使用できるとき、オーディオ ドライバーには、暗証番号 (pin) の既定の設定を変更する必要があります、\_AZALIABUS\_SENDVERBS 送受信するように設定し、オーディオ コーデックから動詞を取得します。 オーディオ コーデックとの通信は、pin の構成の詳細については、オーディオ コーデックはのみ Get 動詞に応答します。

次の例では、パラメーターとして AzCorbeEntry 構造体と、ハンドルを取得し、コーデックから、AzRirbResponse を返す関数を示します。

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

データ型と上記のコード例で使用される構造は、次の例で定義されます。

### <a name="span-idazcorbentryspanspan-idazcorbentryspan-azcorbentry"></a><span id="azcorbentry"></span><span id="AZCORBENTRY"></span> AzCorbEntry

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

### <a name="span-idazrirbentryspanspan-idazrirbentryspan-azrirbentry"></a><span id="azrirbentry"></span><span id="AZRIRBENTRY"></span> AzRirbEntry

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

次の 2 つの構造はコマンドを有効にする動詞転送 IOCTL と共に使用され、応答は、オーディオ ドライバーと HD オーディオ コーデック間で転送。

### <a name="span-idusermodecodeccommandpacketspanspan-idusermodecodeccommandpacketspan-usermodecodeccommandpacket"></a><span id="usermodecodeccommandpacket"></span><span id="USERMODECODECCOMMANDPACKET"></span> UserModeCodecCommandPacket

```cpp
typedef struct _UserModeCodecCommandPacket
{
  ULONG NumCommands;      // number of commands in this packet
  AzCorbEntry Command[1]; // variable length array of verbs
} UserModeCodecCommandPacket;
```

### <a name="span-idusermodecodecresponsepacketspanspan-idusermodecodecresponsepacketspan-usermodecodecresponsepacket"></a><span id="usermodecodecresponsepacket"></span><span id="USERMODECODECRESPONSEPACKET"></span> UserModeCodecResponsePacket

```cpp
typedef struct _UserModeCodecResponsePacket
{
  ULONG NumResponses;       // on successful IOCTL, this will be updated with the number of responses.
  AzRirbEntry Response[1];  // Variable length array of responses. lpOutBuffer param to DeviceIoControl
                            // must point to sufficient space to hold this IOCTL with all its responses 
} UserModeCodecResponsePacket;
```

 

 




