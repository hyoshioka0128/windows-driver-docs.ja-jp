---
title: FSCTL_SUSPEND_OVERLAY 制御コード
description: FSCTL\_SUSPEND\_オーバーレイ コントロールのコードは、バックアップ ソースへのアクセスを防止し、変更または削除することができます、ボリュームに接続されているバックアップ ソースを中断します。
ms.assetid: 5BC73E77-86A0-4A7D-BCBA-F3E8DA980701
keywords:
- FSCTL_SUSPEND_OVERLAY 制御コード インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FSCTL_SUSPEND_OVERLAY
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 839126891ea06998f4260a6f1b10a24c8ffac60e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573172"
---
# <a name="fsctlsuspendoverlay-control-code"></a>FSCTL\_SUSPEND\_オーバーレイ コントロール コード


**FSCTL\_SUSPEND\_オーバーレイ**制御コードは、バックアップ ソースへのアクセスを防止し、変更または削除することができます、ボリュームに接続されているバックアップ ソースを中断します。

この操作を実行するには、呼び出す[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

``` syntax
BOOL 
   WINAPI 
   DeviceIoControl( (HANDLE)       hDevice,         // handle to device
                    (DWORD)        FSCTL_SUSPEND_OVERLAY, // dwIoControlCode
                    (LPDWORD)      lpInBuffer,      // input buffer
                    (DWORD)        nInBufferSize,   // size of input buffer
                    (LPDWORD)      lpOutBuffer,     // output buffer
                    (DWORD)        nOutBufferSize,  // size of output buffer
                    (LPDWORD)      lpBytesReturned, // number of bytes returned
                    (LPOVERLAPPED) lpOverlapped );  // OVERLAPPED structure
```

**Parameters**

<a href="" id="instance--in-"></a>*インスタンス\[で\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)のみです。 呼び出し元の非透過インスタンス ポインター。 このパラメーターは、必要なは、NULL にすることはできません。

<a href="" id="fileobject--in-"></a>*FileObject\[で\]*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)のみです。 オーバーレイが更新されるボリュームのファイル ポインター オブジェクト。 このパラメーターは、必要なは、NULL にすることはできません。

<a href="" id="filehandle--in-"></a>*FileHandle\[で\]*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみです。 オーバーレイが更新されるボリュームのハンドル。 このパラメーターは、必要なは、NULL にすることはできません。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode\[で\]*  
操作の制御コード。 使用**FSCTL\_SUSPEND\_オーバーレイ**この操作にします。

<a href="" id="inputbuffer"></a>*InputBuffer*  
含める必要がありますが、入力バッファーへのポインターを[ **WOF\_外部\_情報**](https://msdn.microsoft.com/library/windows/hardware/dn632452)構造体。 追加のプロバイダー固有のデータは後すぐに、必要な場合に**WOF\_外部\_情報**します。 プロバイダーが、WIM ファイルの場合、 [ **WIM\_プロバイダー\_SUSPEND\_オーバーレイ\_入力**](https://msdn.microsoft.com/library/windows/hardware/mt426740)構造が後に含まれる**WOF\_外部\_情報**します。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength\[で\]*  
設定**sizeof**([**WOF\_外部\_情報**](https://msdn.microsoft.com/library/windows/hardware/dn632452)) さらに、追加のプロバイダーの入力データのサイズ。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer\[アウト\]*  
使用されません。 NULL に設定します。

<a href="" id="outputbufferlength--in-"></a>*OutputBufferLength\[で\]*  
0 に設定します。

<a name="status-block"></a>ステータス ブロック
------------

[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)ステータスを返します\_操作が成功した場合は成功します。 それ以外の場合、適切な関数では NTSTATUS 値は次のいずれかを返す可能性があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">項目</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>リクエスターでは、管理者特権はありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p>によって示される入力バッファーの長さ<em>InputBuffer</em>とで指定した<em>InputBufferLength</em>、小さすぎます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_INTERNAL_ERROR</strong></p></td>
<td align="left"><p>要求されたボリュームにアクセスできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_DEVICE_REQUEST</strong></p></td>
<td align="left"><p>バックアップ サービスが存在しないか開始されていません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

削除するバックアップ ソースは、Windows Imaging Format (WIM) ファイルが、入力バッファーに格納されます、 [ **WOF\_外部\_情報**](https://msdn.microsoft.com/library/windows/hardware/dn632452)構造体の後に、 [ **WIM\_プロバイダー\_SUSPEND\_オーバーレイ\_入力**](https://msdn.microsoft.com/library/windows/hardware/mt426740)構造体。 *InputBufferLength*ここでは、 **sizeof**(WOF\_外部\_情報) + **sizeof**([**WIM\_プロバイダー\_削除\_オーバーレイ\_入力**](https://msdn.microsoft.com/library/windows/hardware/dn632450))。 **DataSourceId**値**WIM\_プロバイダー\_SUSPEND\_オーバーレイ\_入力**WIM ファイルので以前に追加する必要があります[ **FSCTL\_追加\_オーバーレイ**](fsctl-add-overlay.md)要求。

追加のバックアップ プロバイダーは、独自の特定の入力パラメーターの構造を定義します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h (Ntifs.h または Fltkernel.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FSCTL\_削除\_オーバーレイ**](fsctl-remove-overlay.md)

[**FSCTL\_UPDATE\_オーバーレイ**](fsctl-update-overlay.md)

[**FSCTL\_取得\_外部\_バックアップ**](fsctl-get-external-backing.md)

[**FSCTL\_設定\_外部\_バックアップ**](fsctl-set-external-backing.md)

 

 






