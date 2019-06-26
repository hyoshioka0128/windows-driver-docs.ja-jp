---
title: FSCTL_REMOVE_OVERLAY 制御コード
description: FSCTL\_削除\_オーバーレイ コントロールのコードは、ボリュームからバックアップ ソースを削除します。
ms.assetid: 9AB1DD06-AFB3-45AF-8139-14B60076D63A
keywords:
- FSCTL_REMOVE_OVERLAY 制御コード インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FSCTL_REMOVE_OVERLAY
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 921a70541e7018f0cd35996cc756ced96aec1c16
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380066"
---
# <a name="fsctlremoveoverlay-control-code"></a>FSCTL\_削除\_オーバーレイ コントロール コード


**FSCTL\_削除\_オーバーレイ**制御コードは、ボリュームからバックアップ ソースを削除します。

この操作を実行するには、呼び出す[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

**Parameters**

<a href="" id="instance--in-"></a>*インスタンス\[で\]*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)のみです。 呼び出し元の非透過インスタンス ポインター。 このパラメーターは、必要なは、NULL にすることはできません。

<a href="" id="fileobject--in-"></a>*FileObject\[で\]*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)のみです。 オーバーレイを削除するボリュームのファイル ポインター オブジェクト。 このパラメーターは、必要なは、NULL にすることはできません。

<a href="" id="filehandle--in-"></a>*FileHandle\[で\]*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみです。 オーバーレイを削除するボリュームのハンドル。 このパラメーターは、必要なは、NULL にすることはできません。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode\[で\]*  
操作の制御コード。 使用**FSCTL\_削除\_オーバーレイ**この操作にします。

<a href="" id="inputbuffer"></a>*InputBuffer*  
含める必要がありますが、入力バッファーへのポインターを[ **WOF\_外部\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_wof_external_info)構造体。 追加のプロバイダー固有のデータは後すぐに、必要な場合に**WOF\_外部\_情報**します。 プロバイダーが、WIM ファイルの場合、 [ **WIM\_プロバイダー\_削除\_オーバーレイ\_入力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_wim_provider_remove_overlay_input)構造が後に含まれる**WOF\_外部\_情報**します。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength\[で\]*  
設定**sizeof**([**WOF\_外部\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_wof_external_info)) さらに、追加のプロバイダーの入力データのサイズ。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer\[アウト\]*  
使用されていません。 NULL に設定します。

<a href="" id="outputbufferlength--in-"></a>*OutputBufferLength\[で\]*  
0 に設定します。

<a name="status-block"></a>ステータス ブロック
------------

[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)ステータスを返します\_操作が成功した場合は成功します。 それ以外の場合、適切な関数では NTSTATUS 値は次のいずれかを返す可能性があります。

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
<td align="left"><p>によって示される出力バッファーの長さ<em>OutputBuffer</em>とで指定した<em>OutputBufferLength</em>、小さすぎます。</p></td>
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

 

<a name="remarks"></a>注釈
-------

削除するバックアップ ソースは、Windows Imaging Format (WIM) ファイルが、入力バッファーに格納されます、 [ **WOF\_外部\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_wof_external_info)構造体の後に、 [ **WIM\_プロバイダー\_削除\_オーバーレイ\_入力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_wim_provider_remove_overlay_input)構造体。 *InputBufferLength*ここでは、 **sizeof**(WOF\_外部\_情報) + **sizeof**(**WIM\_プロバイダー\_削除\_オーバーレイ\_入力**)。 **DataSourceId**値**WIM\_プロバイダー\_削除\_オーバーレイ\_入力**WIM ファイルが以前に追加する必要があります、 [**FSCTL\_追加\_オーバーレイ**](fsctl-add-overlay.md)要求。

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
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 8.1 Update 以降を利用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h (Ntifs.h または Fltkernel.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FSCTL\_SUSPEND\_オーバーレイ**](fsctl-suspend-overlay.md)

[**FSCTL\_UPDATE\_オーバーレイ**](fsctl-update-overlay.md)

[**FSCTL\_取得\_外部\_バックアップ**](fsctl-get-external-backing.md)

[**FSCTL\_設定\_外部\_バックアップ**](fsctl-set-external-backing.md)

 

 






