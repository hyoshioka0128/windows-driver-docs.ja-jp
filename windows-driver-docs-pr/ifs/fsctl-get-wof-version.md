---
title: FSCTL_GET_WOF_VERSION 制御コード
description: FSCTL\_GET\_WOF\_バージョンの i/o 制御コード (IOCTL) を使用して、特定のプロバイダーをサポートするために使用されるドライバーのバージョンを照会します。
ms.assetid: 0E3C3C7E-2A89-4CA8-8741-7C057E063155
keywords:
- FSCTL_GET_WOF_VERSION 制御コードのインストール可能なファイルシステムドライバー
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
ms.openlocfilehash: a479f3a6bd0d0283e82847725b77d9fc7a1f31cc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841300"
---
# <a name="fsctl_get_wof_version-control-code"></a>FSCTL\_\_WOF\_バージョン管理コードを取得する


**FSCTL\_GET\_WOF\_バージョン**の i/o 制御コード (IOCTL) を使用して、特定のプロバイダーをサポートするために使用されるドライバーのバージョンを照会します。

この操作を実行するには、次のパラメーターを使用して[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を呼び出します。

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

**パラメーター**

<a href="" id="hdevice--in-"></a>*hDevice \[\]*  
デバイスへのハンドル。 デバイスハンドルを取得するには、 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)関数または同様の API を呼び出します。

<a href="" id="dwiocontrolcode--in-"></a> *\]の dwIoControlCode \[*  
操作の制御コード。 この操作には、FSCTL\_使用して **\_WOF\_バージョンを取得**してください。

<a href="" id="lpinbuffer"></a>*lpInBuffer*  
操作の入力バッファー。 これは、 [**WOF\_外部\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)構造体へのポインターです。

<a href="" id="ninbuffersize--in-"></a> *\]の nInBufferSize \[*  
入力バッファーのサイズ (バイト単位)。 これは**sizeof**([**WOF\_外部\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)) にする必要があります。

<a href="" id="lpoutbuffer--out-"></a>*lpOutBuffer \[out\]*  
操作の出力バッファー。 これは、 [**WOF\_バージョン\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_version_info)構造体へのポインターです。

<a href="" id="noutbuffersize--in-"></a> *\]の nOutBufferSize \[*  
出力バッファーのサイズ (バイト単位)。 これは**sizeof**([**WOF\_VERSION\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_version_info)) である必要があります。

<a href="" id="lpbytesreturned--out-"></a>*lpBytesReturned \[out\]を返しました*  
**LPDWORD**

出力バッファーに格納されているデータのサイズ (バイト単位) を受け取る変数へのポインター。

出力バッファーが小さすぎると、呼び出しが失敗し、 [**GetLastError**](https://docs.microsoft.com/windows/desktop/api/errhandlingapi/nf-errhandlingapi-getlasterror)が**エラー\_\_バッファーが不足**し、 *lpbytesreturned* 0 を返します。

*LpOverlapped*が**null**の場合、 *lpbytesreturned* **null**にすることはできません。 操作によって出力データが返されず、 *Lpoutbuffer*が**NULL**の場合でも、 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)は*lpoutbuffer*使用して返されます。 このような操作を行った後、*返された Lpbytesreturned*値は無意味になります。

*LpOverlapped*が**null**でない場合は、 *lpbytesreturned* **null**になることがあります。 このパラメーターが**NULL**でなく、操作がデータを返す場合は、重複操作が完了するまで、 *lpbytesreturned 返さ*れることは意味がありません。 返されるバイト数を取得するには、 [**GetOverlappedResult**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-getoverlappedresult)を呼び出します。 *Hdevice*パラメーターが i/o 完了ポートに関連付けられている場合は、 [**GetQueuedCompletionStatus**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-getqueuedcompletionstatus)を呼び出すことによって返されるバイト数を取得できます。

<a href="" id="lpoverlapped--in-"></a> *\]の lpOverlapped \[*  
**LPOVERLAPPED**

[**オーバーラップ**](https://docs.microsoft.com/windows/desktop/api/minwinbase/ns-minwinbase-_overlapped)された構造体へのポインター。

**ファイル\_\_フラグ**を指定せずに*hdevice*を開いた場合、 *lpOverlapped*は無視されます。

*Hdevice*が**ファイル\_フラグ**を使用して開かれている場合は、重複フラグ\_、この操作は、オーバーラップ (非同期) 操作として実行されます。 この場合、 *lpOverlapped*は、イベントオブジェクトへのハンドルを含む有効な[**オーバーラップ**](https://docs.microsoft.com/windows/desktop/api/minwinbase/ns-minwinbase-_overlapped)構造体を指す必要があります。 それ以外の場合、関数は予期しない方法で失敗します。

オーバーラップ操作の場合、 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)はすぐに制御を返し、操作が完了するとイベントオブジェクトを通知します。 それ以外の場合、この関数は、操作が完了するかエラーが発生するまで、を返しません。

<a name="status-block"></a>状態ブロック
------------

操作が正常に完了した場合、 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)は0以外の値を返します。

操作が失敗した場合、または保留中の場合、 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)は0を返します。 エラーの詳細情報を取得するには、 [**GetLastError**](https://docs.microsoft.com/windows/desktop/api/errhandlingapi/nf-errhandlingapi-getlasterror)を呼び出します。

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 10 以降で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ヘッダー</p></td>
<td align="left">Ntifs (Ntifs または Fltkernel .h を含む)</td>
</tr>
</tbody>
</table>

 

 





