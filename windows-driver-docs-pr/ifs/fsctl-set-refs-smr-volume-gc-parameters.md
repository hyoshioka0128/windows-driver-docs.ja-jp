---
title: FSCTL_SET_REFS_SMR_VOLUME_GC_PARAMETERS 制御コード
description: FSCTL\_設定\_REFS\_SMR\_ボリューム\_GC\_Shingled 磁気記録 (SMR) ボリューム上のガベージ コレクションにコントロールのコードを制御するパラメーター。
ms.assetid: 782542C4-CFC5-4BF7-AF38-3247A3AC6AB9
keywords:
- FSCTL_SET_REFS_SMR_VOLUME_GC_PARAMETERS は、ファイル システム ドライバーがインストール可能なコードを制御します。
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
ms.openlocfilehash: 8f29c702bb77cc3027d2f4a786911f0531f8f9bc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550804"
---
# <a name="fsctlsetrefssmrvolumegcparameters-control-code"></a>FSCTL\_設定\_REFS\_SMR\_ボリューム\_GC\_コードを制御するパラメーター


**FSCTL\_設定\_REFS\_SMR\_ボリューム\_GC\_パラメーター**制御コード、Shingled 磁気記録 (でガベージ コレクションの制御SMR) ボリューム。

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

*hDevice* \[で\]  
デバイスへのハンドル。 デバイス ハンドルを取得する呼び出し、 [ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)関数。

*dwIoControlCode* \[in\]  
操作の制御コード。 使用**FSCTL\_設定\_REFS\_SMR\_ボリューム\_GC\_パラメーター**この操作にします。

*lpInBuffer*   
呼び出し元が割り当てたへのポインター [ **REFS\_SMR\_ボリューム\_GC\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/mt842917)構造体。

*nInBufferSize* \[in\]  
(バイト単位)、入力バッファーのサイズ。

*lpOutBuffer* \[アウト\]  
この操作では使用されません。設定**NULL**します。

*nOutBufferSize* \[in\]  
この操作では使用されません。0 に設定します。

*lpBytesReturned* \[out\]  
この操作では使用されません。設定**NULL**します。

*lpOverlapped* \[in\]  
ポインター、 [ **OVERLAPPED** ](https://msdn.microsoft.com/library/windows/desktop/ms684342)構造体。

場合*hDevice*を指定せずに開かれた**ファイル\_フラグ\_OVERLAPPED**、 *lpOverlapped*は無視されます。

場合*hDevice*で開かれた、**ファイル\_フラグ\_OVERLAPPED**フラグは、操作がオーバー ラップ (非同期) 操作として実行します。 この場合、 *lpOverlapped*有効 をポイントする必要があります[ **OVERLAPPED** ](https://msdn.microsoft.com/library/windows/desktop/ms684342)イベント オブジェクトへのハンドルを含む構造体。 それ以外の場合、関数は、予測できない方法で失敗します。

重複した操作は、 [ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)を即座に返します、操作が完了したときに、イベント オブジェクトがシグナル状態とします。 それ以外の場合、操作が完了したか、エラーが発生するまでには、この関数は返されません。

<a name="return-value"></a>戻り値
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
<td align="left"><p>Windows 10 バージョン 1709 以降を使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">WinIoctl.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**DeviceIoControl**](https://msdn.microsoft.com/library/windows/desktop/aa363216)

 

 






