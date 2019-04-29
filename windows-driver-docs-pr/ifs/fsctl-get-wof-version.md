---
title: FSCTL_GET_WOF_VERSION 制御コード
description: FSCTL\_取得\_WOF\_バージョン I/O 制御コード (IOCTL) は、特定のプロバイダーをサポートするために使用されているドライバーのバージョンをクエリに使用されます。
ms.assetid: 0E3C3C7E-2A89-4CA8-8741-7C057E063155
keywords:
- FSCTL_GET_WOF_VERSION 制御コード インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FSCTL_GET_WOF_VERSION
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73dc3150b48ed350168e619a99e52ffa8f28f08f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324609"
---
# <a name="fsctlgetwofversion-control-code"></a>FSCTL\_取得\_WOF\_バージョン制御コード


**FSCTL\_取得\_WOF\_バージョン**I/O 制御コード (IOCTL) は、特定のプロバイダーをサポートするために使用されているドライバーのバージョンをクエリに使用されます。

この操作を実行するには、呼び出す[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

``` syntax
BOOL 
   WINAPI 
   DeviceIoControl( (HANDLE)       hDevice,         // handle to device
                    (DWORD)        FSCTL_GET_WOF_VERSION, // dwIoControlCode
                    (LPDWORD)      lpInBuffer,      // input buffer
                    (DWORD)        nInBufferSize,   // size of input buffer
                    (LPDWORD)      lpOutBuffer,     // output buffer
                    (DWORD)        nOutBufferSize,  // size of output buffer
                    (LPDWORD)      lpBytesReturned, // number of bytes returned
                    (LPOVERLAPPED) lpOverlapped );  // OVERLAPPED structure
```

**Parameters**

<a href="" id="hdevice--in-"></a>*hDevice\[で\]*  
デバイスへのハンドル。 デバイス ハンドルを取得する呼び出し、 [ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)関数または同様の API。

<a href="" id="dwiocontrolcode--in-"></a>*dwIoControlCode\[で\]*  
操作の制御コード。 使用**FSCTL\_取得\_WOF\_バージョン**この操作にします。

<a href="" id="lpinbuffer"></a>*lpInBuffer*  
操作の入力バッファー。 これへのポインターを[ **WOF\_外部\_情報**](https://msdn.microsoft.com/library/windows/hardware/dn632452)構造体。

<a href="" id="ninbuffersize--in-"></a>*nInBufferSize\[で\]*  
入力バッファーのバイト単位のサイズ。 これは、アカウントは**sizeof**([**WOF\_外部\_情報**](https://msdn.microsoft.com/library/windows/hardware/dn632452))。

<a href="" id="lpoutbuffer--out-"></a>*lpOutBuffer\[アウト\]*  
操作の出力バッファー。 これへのポインターを[ **WOF\_バージョン\_情報**](https://msdn.microsoft.com/library/windows/hardware/mt426742)構造体。

<a href="" id="noutbuffersize--in-"></a>*nOutBufferSize\[で\]*  
出力バッファーのバイト単位のサイズ。 これは、アカウントは**sizeof**([**WOF\_バージョン\_情報**](https://msdn.microsoft.com/library/windows/hardware/mt426742))。

<a href="" id="lpbytesreturned--out-"></a>*lpBytesReturned\[アウト\]*  
**LPDWORD**

(バイト単位)、出力バッファーに格納されているデータのサイズを受け取る変数へのポインター。

出力バッファーが小さすぎる場合は、呼び出しが失敗した、 [ **GetLastError** ](https://msdn.microsoft.com/library/windows/desktop/ms679360)返します**エラー\_不十分\_バッファー**、および*lpBytesReturned*は 0 です。

場合*lpOverlapped*は**NULL**、 *lpBytesReturned*することはできません**NULL**します。 でもときに操作を返しません出力データと*lpOutBuffer*は**NULL**、 [ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)活用*lpBytesReturned*します。 このような操作の値の後に*lpBytesReturned*は意味がありません。

場合*lpOverlapped*ない**NULL**、 *lpBytesReturned*できる**NULL**します。 このパラメーターがない場合**NULL**操作は、そのデータを返します*lpBytesReturned*オーバー ラップ処理が完了するまでは無意味です。 返されるバイト数を取得する[ **GetOverlappedResult**](https://msdn.microsoft.com/library/windows/desktop/ms683209)します。 場合、 *hDevice*パラメーターは、I/O 完了ポートに関連付け、呼び出すことによって返されるバイト数を取得する[ **GetQueuedCompletionStatus**](https://msdn.microsoft.com/library/windows/desktop/aa364986)します。

<a href="" id="lpoverlapped--in-"></a>*lpOverlapped\[で\]*  
**LPOVERLAPPED**

ポインター、 [ **OVERLAPPED** ](https://msdn.microsoft.com/library/windows/desktop/ms684342)構造体。

場合*hDevice*を指定せずに開かれた**ファイル\_フラグ\_OVERLAPPED**、 *lpOverlapped*は無視されます。

場合*hDevice*で開かれた、**ファイル\_フラグ\_OVERLAPPED**フラグは、操作がオーバー ラップ (非同期) 操作として実行します。 この場合、 *lpOverlapped*有効 をポイントする必要があります[ **OVERLAPPED** ](https://msdn.microsoft.com/library/windows/desktop/ms684342)イベント オブジェクトへのハンドルを含む構造体。 それ以外の場合、関数は、予測できない方法で失敗します。

重複した操作は、 [ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)を即座に返します、操作が完了したときに、イベント オブジェクトがシグナル状態とします。 それ以外の場合、操作が完了したか、エラーが発生するまでには、この関数は返されません。

<a name="status-block"></a>ステータス ブロック
------------

操作が正常に完了した場合[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216) 0 以外の値を返します。

操作は、障害が発生したり、保留中で[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)は 0 を返します。 拡張エラー情報を取得するには呼び出します[ **GetLastError**](https://msdn.microsoft.com/library/windows/desktop/ms679360)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 10 以降で利用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h (Ntifs.h または Fltkernel.h を含む)</td>
</tr>
</tbody>
</table>

 

 





