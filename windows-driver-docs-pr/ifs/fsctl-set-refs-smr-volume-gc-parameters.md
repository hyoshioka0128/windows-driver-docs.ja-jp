---
title: FSCTL_SET_REFS_SMR_VOLUME_GC_PARAMETERS 制御コード
description: FSCTL\_SET\_REFS\_SMR\_ボリューム\_GC\_PARAMETERS 制御コードは、Shingled 磁気記録 (SMR) ボリュームでガベージコレクションを制御します。
ms.assetid: 782542C4-CFC5-4BF7-AF38-3247A3AC6AB9
keywords:
- FSCTL_SET_REFS_SMR_VOLUME_GC_PARAMETERS コントロールコードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_SET_REFS_SMR_VOLUME_GC_PARAMETERS
api_location:
- WinIoctl.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7931a45815cf4ce94eae34e7ceb52252e793675d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841248"
---
# <a name="fsctl_set_refs_smr_volume_gc_parameters-control-code"></a>FSCTL\_\_REFS\_SMR\_ボリューム\_GC\_パラメーター制御コードに設定します。


**FSCTL\_SET\_REFS\_SMR\_ボリューム\_GC\_PARAMETERS**制御コードは、Shingled 磁気記録 (SMR) ボリュームでガベージコレクションを制御します。

```ManagedCPlusPlus
BOOL
   DeviceIoControl( (HANDLE)       hDevice,         // handle to volume
                    FSCTL_SET_REFS_SMR_VOLUME_GC_PARAMETERS, // dwIoControlCode
                    (LPDWORD)      lpInBuffer,      // input buffer
                    (DWORD)        nInBufferSize,   // size of input buffer
                     NULL,     // output buffer
                     0,  // size of output buffer
                    (LPDWORD)      lpBytesReturned, // number of bytes returned
                    (LPOVERLAPPED) lpOverlapped );  // OVERLAPPED structure
```

<a name="parameters"></a>パラメーター
----------

*Hdevice* \[\]  
デバイスへのハンドル。 デバイスハンドルを取得するには、 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)関数を呼び出します。

\] の*Dwiocontrolcode* \[  
操作の制御コード。 この操作には、FSCTL\_使用して、 **\_REFS\_SMR\_ボリューム\_GC\_パラメーターを設定**します。

*Lpinbuffer*   
呼び出し元が割り当てた[**REFS\_SMR\_ボリューム\_GC\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_refs_smr_volume_gc_parameters)構造体へのポインター。

\] の*nInBufferSize* \[  
入力バッファーのサイズ (バイト単位)。

*Lpoutbuffer* \[out\]  
この操作では使用されません。を**NULL**に設定します。

\] の*Noutbuffersize* \[  
この操作では使用されません。を0に設定します。

*Lpbytesreturned* \[out\] を返しました  
この操作では使用されません。を**NULL**に設定します。

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

 

 






