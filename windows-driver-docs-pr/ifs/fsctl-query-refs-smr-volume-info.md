---
title: FSCTL_QUERY_REFS_SMR_VOLUME_INFO 制御コード
description: FSCTL\_クエリ\_REFS\_SMR\_ボリューム\_情報制御コードは、領域とガベージコレクションアクティビティの現在の状態を Shingled 磁気記録 (SMR) ボリュームに照会します。
ms.assetid: 1318CF90-2449-407E-8C9E-825E571F4CDD
keywords:
- FSCTL_QUERY_REFS_SMR_VOLUME_INFO 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_QUERY_REFS_SMR_VOLUME_INFO
api_location:
- WinIoctl.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1aed05f8f633044b3bfb6a7beeb65ac464f62624
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841280"
---
# <a name="fsctl_query_refs_smr_volume_info-control-code"></a>FSCTL\_クエリ\_REFS\_SMR\_ボリューム\_情報制御コード


**FSCTL\_クエリ\_REFS\_SMR\_ボリューム\_情報**制御コードは、領域とガベージコレクションアクティビティの現在の状態を Shingled 磁気記録 (smr) ボリュームに照会します。

この操作を実行するには、次のパラメーターを使用して[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)関数を呼び出します。

```ManagedCPlusPlus
BOOL 
DeviceIoControl( (HANDLE)       hDevice,         // handle to device
                    (DWORD)        FSCTL_QUERY_REFS_SMR_VOLUME_INFO, // dwIoControlCode
                    (LPDWORD)      lpInBuffer,      // input buffer
                    (DWORD)        nInBufferSize,   // size of input buffer
                    (LPDWORD)      lpOutBuffer,     // output buffer
                    (DWORD)        nOutBufferSize,  // size of output buffer
                    (LPDWORD)      lpBytesReturned, // number of bytes returned
                    (LPOVERLAPPED) lpOverlapped );  // OVERLAPPED structure
```

<a name="parameters"></a>パラメーター
----------

*Hdevice* \[\]  
デバイスへのハンドル。 デバイスハンドルを取得するには、 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)関数を呼び出します。

\] の*Dwiocontrolcode* \[  
操作の制御コード。 この操作には、 **FSCTL\_クエリ\_REFS\_SMR\_ボリューム\_情報**を使用します。

*Lpinbuffer*   
この操作では使用されません。を**NULL**に設定します。

\] の*nInBufferSize* \[  
この操作では使用されません。を0に設定します。

*Lpoutbuffer* \[out\]  
領域およびガベージコレクションアクティビティのボリュームの現在の状態を指定する参照[ **\_SMR\_ボリューム\_情報\_出力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_refs_smr_volume_info_output)構造体を受け取るバッファーへのポインター。

\] の*Noutbuffersize* \[  
出力バッファーのサイズ (バイト単位)。

*Lpbytesreturned* \[out\] を返しました  
出力バッファーに格納されているデータのサイズ (バイト単位) を受け取る変数へのポインター。

出力バッファーが小さすぎると、呼び出しが失敗し、 [**GetLastError**](https://docs.microsoft.com/windows/desktop/api/errhandlingapi/nf-errhandlingapi-getlasterror)が**エラー\_\_バッファーが不足**し、 *lpbytesreturned* 0 を返します。

*LpOverlapped*が**null**の場合、 *lpbytesreturned* **null**にすることはできません。 操作によって出力データが返されず、 *Lpoutbuffer*が**NULL**の場合でも、 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)は*lpoutbuffer*使用して返されます。 このような操作を行った後、*返された Lpbytesreturned*値は無意味になります。

*LpOverlapped*が**null**でない場合は、 *lpbytesreturned* **null**になることがあります。 このパラメーターが**NULL**でなく、操作がデータを返す場合は、重複操作が完了するまで、 *lpbytesreturned 返さ*れることは意味がありません。 返されるバイト数を取得するには、 [**GetOverlappedResult**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-getoverlappedresult)を呼び出します。 *Hdevice*パラメーターが i/o 完了ポートに関連付けられている場合は、 [**GetQueuedCompletionStatus**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-getqueuedcompletionstatus)を呼び出すことによって返されるバイト数を取得できます。

\] の*lpOverlapped* \[  
[**オーバーラップ**](https://docs.microsoft.com/windows/desktop/api/minwinbase/ns-minwinbase-_overlapped)された構造体へのポインター。

**ファイル\_\_フラグ**を指定せずに*hdevice*を開いた場合、 *lpOverlapped*は無視されます。

*Hdevice*が**ファイル\_フラグ**を使用して開かれている場合は、重複フラグ\_、この操作は、オーバーラップ (非同期) 操作として実行されます。 この場合、 *lpOverlapped*は、イベントオブジェクトへのハンドルを含む有効な[**オーバーラップ**](https://docs.microsoft.com/windows/desktop/api/minwinbase/ns-minwinbase-_overlapped)構造体を指す必要があります。 それ以外の場合、関数は予期しない方法で失敗します。

オーバーラップ操作の場合、 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)はすぐに制御を返し、操作が完了するとイベントオブジェクトを通知します。 それ以外の場合、この関数は、操作が完了するかエラーが発生するまで、を返しません。

<a name="return-value"></a>戻り値
------------

操作が正常に完了した場合、 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)は0以外の値を返します。

操作が失敗した場合、または保留中の場合、 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)は0を返します。 エラーの詳細情報を取得するには、 [**GetLastError**](https://docs.microsoft.com/windows/desktop/api/errhandlingapi/nf-errhandlingapi-getlasterror)を呼び出します。

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
<td align="left"><p>Windows 10 バージョン1709以降で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">WinIoctl. h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)

[**REFS\_SMR\_ボリューム\_情報\_出力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_refs_smr_volume_info_output)

[**REFS\_SMR\_ボリューム\_GC\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ne-ntifs-_refs_smr_volume_gc_state)

 

 






