---
title: FSCTL_QUERY_REFS_SMR_VOLUME_INFO 制御コード
description: FSCTL\_クエリ\_REFS\_SMR\_ボリューム\_情報制御コードが Shingled 磁気記録 (SMR) ボリュームの領域とガベージ コレクションのアクティビティの現在の状態をクエリします。
ms.assetid: 1318CF90-2449-407E-8C9E-825E571F4CDD
keywords:
- FSCTL_QUERY_REFS_SMR_VOLUME_INFO 制御コード インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 38bee14a7e8a9c932f2a2d0ba0a4e9d212da94a2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380987"
---
# <a name="fsctlqueryrefssmrvolumeinfo-control-code"></a>FSCTL\_クエリ\_REFS\_SMR\_ボリューム\_情報制御コード


**FSCTL\_クエリ\_REFS\_SMR\_ボリューム\_情報**制御コードの Shingled 磁気記録 (SMR) ボリュームの空き領域の現在の状態をクエリし、ガベージ コレクションのアクティビティ。

この操作を実行するには、呼び出し、 [ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)関数は次のパラメーター。

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

*hDevice* \[で\]  
デバイスへのハンドル。 デバイス ハンドルを取得する呼び出し、 [ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)関数。

*dwIoControlCode* \[in\]  
操作の制御コード。 使用**FSCTL\_クエリ\_REFS\_SMR\_ボリューム\_情報**この操作にします。

*lpInBuffer*   
この操作では使用されません。設定**NULL**します。

*nInBufferSize* \[in\]  
この操作では使用されません。0 に設定します。

*lpOutBuffer* \[アウト\]  
受け取るバッファーへのポインターを[ **REFS\_SMR\_ボリューム\_情報\_出力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_refs_smr_volume_info_output)領域のボリュームの現在の状態を指定する構造体ガベージ コレクションのアクティビティ。

*nOutBufferSize* \[in\]  
(バイト単位)、出力バッファーのサイズ。

*lpBytesReturned* \[out\]  
(バイト単位)、出力バッファーに格納されているデータのサイズを受け取る変数へのポインター。

出力バッファーが小さすぎる場合は、呼び出しが失敗した、 [ **GetLastError** ](https://docs.microsoft.com/windows/desktop/api/errhandlingapi/nf-errhandlingapi-getlasterror)返します**エラー\_不十分\_バッファー**、および*lpBytesReturned*は 0 です。

場合*lpOverlapped*は**NULL**、 *lpBytesReturned*することはできません**NULL**します。 でもときに操作を返しません出力データと*lpOutBuffer*は**NULL**、 [ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)活用*lpBytesReturned*します。 このような操作の値の後に*lpBytesReturned*は意味がありません。

場合*lpOverlapped*ない**NULL**、 *lpBytesReturned*できる**NULL**します。 このパラメーターがない場合**NULL**操作は、そのデータを返します*lpBytesReturned*オーバー ラップ処理が完了するまでは無意味です。 返されるバイト数を取得する[ **GetOverlappedResult**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-getoverlappedresult)します。 場合、 *hDevice*パラメーターは、I/O 完了ポートに関連付け、呼び出すことによって返されるバイト数を取得する[ **GetQueuedCompletionStatus**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-getqueuedcompletionstatus)します。

*lpOverlapped* \[in\]  
ポインター、 [ **OVERLAPPED** ](https://docs.microsoft.com/windows/desktop/api/minwinbase/ns-minwinbase-_overlapped)構造体。

場合*hDevice*を指定せずに開かれた**ファイル\_フラグ\_OVERLAPPED**、 *lpOverlapped*は無視されます。

場合*hDevice*で開かれた、**ファイル\_フラグ\_OVERLAPPED**フラグは、操作がオーバー ラップ (非同期) 操作として実行します。 この場合、 *lpOverlapped*有効 をポイントする必要があります[ **OVERLAPPED** ](https://docs.microsoft.com/windows/desktop/api/minwinbase/ns-minwinbase-_overlapped)イベント オブジェクトへのハンドルを含む構造体。 それ以外の場合、関数は、予測できない方法で失敗します。

重複した操作は、 [ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)を即座に返します、操作が完了したときに、イベント オブジェクトがシグナル状態とします。 それ以外の場合、操作が完了したか、エラーが発生するまでには、この関数は返されません。

<a name="return-value"></a>戻り値
------------

操作が正常に完了した場合[ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol) 0 以外の値を返します。

操作は、障害が発生したり、保留中で[ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)は 0 を返します。 拡張エラー情報を取得するには呼び出します[ **GetLastError**](https://docs.microsoft.com/windows/desktop/api/errhandlingapi/nf-errhandlingapi-getlasterror)します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 10 バージョン 1709 以降を使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">WinIoctl.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)

[**REFS\_SMR\_ボリューム\_情報\_出力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_refs_smr_volume_info_output)

[**REFS\_SMR\_ボリューム\_GC\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ne-ntifs-_refs_smr_volume_gc_state)

 

 






