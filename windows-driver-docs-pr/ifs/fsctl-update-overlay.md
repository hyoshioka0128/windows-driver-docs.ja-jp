---
title: FSCTL_UPDATE_OVERLAY 制御コード
description: FSCTL\_UPDATE\_オーバーレイコントロールコードは、ボリュームにアタッチされているバッキングソースの新しいデータソース識別子を更新します。
ms.assetid: 2A420AE7-68CA-4B6A-82D2-C4C39A892F16
keywords:
- FSCTL_UPDATE_OVERLAY 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_UPDATE_OVERLAY
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb2d0b6724285bd7626496eaecea1769d6d0cf50
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841240"
---
# <a name="fsctl_update_overlay-control-code"></a>FSCTL\_UPDATE\_オーバーレイコントロールコード


**FSCTL\_UPDATE\_オーバーレイ**コントロールコードは、ボリュームにアタッチされているバッキングソースの新しいデータソース識別子を更新します。

この操作を実行するには、次のパラメーターを使用して[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を呼び出します。

**Parameters**

<a href="" id="instance--in-"></a> *\]のインスタンス \[*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 呼び出し元の非透過インスタンスポインター。 このパラメーターは必須であり、NULL にすることはできません。

<a href="" id="fileobject--in-"></a> *\]の FileObject \[*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 オーバーレイを更新するボリュームのファイルポインターオブジェクト。 このパラメーターは必須であり、NULL にすることはできません。

<a href="" id="filehandle--in-"></a> *\]の FileHandle \[*  
[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみ。 オーバーレイが更新されるボリュームのハンドル。 このパラメーターは必須であり、NULL にすることはできません。

<a href="" id="fscontrolcode--in-"></a> *\]の FsControlCode \[*  
操作の制御コード。 この操作には、FSCTL\_使用して **\_オーバーレイを更新**してください。

<a href="" id="inputbuffer"></a>*InputBuffer*  
入力バッファーへのポインター。これには、 [**WOF\_外部\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)構造体が含まれている必要があります。 必要に応じて、追加のプロバイダー固有のデータは、 **WOF\_外部\_情報**に含まれます。 プロバイダーが WIM ファイルの場合、 [**wim\_プロバイダー\_更新\_オーバーレイ\_入力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_update_overlay_input)構造は、 **WOF\_外部\_情報**に含まれています。

<a href="" id="inputbufferlength--in-"></a> *\]内の InputBufferLength \[*  
**Sizeof**([**WOF\_外部\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)) に、追加のプロバイダー入力データのサイズを加えた値に設定します。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[out\]*  
使用しません。 を NULL に設定します。

<a href="" id="outputbufferlength--in-"></a> *\]の OutputBufferLength \[*  
を0に設定します。

<a name="status-block"></a>ステータス ブロック
------------

[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)は、操作が成功した場合に STATUS\_SUCCESS を返します。 それ以外の場合、適切な関数は、次のいずれかの NTSTATUS 値を返す可能性があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">用語</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>STATUS_ACCESS_DENIED</strong></p></td>
<td align="left"><p>要求元には管理者特権がありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p><em>InputBuffer</em>によってポイントされ、 <em>inputbufferlength</em>によって指定された入力バッファーの長さが小さすぎます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_INTERNAL_ERROR</strong></p></td>
<td align="left"><p>要求されたボリュームにアクセスできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_DEVICE_REQUEST</strong></p></td>
<td align="left"><p>バッキングサービスが存在しないか、開始されていません。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

更新するデータソースが Windows Imaging Format (WIM) ファイルの場合、入力バッファーには、 [**WOF\_外部\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)構造体の後に[**wim\_プロバイダー\_更新\_オーバーレイ\_入力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_update_overlay_input)が格納されます。データ. この場合、 *Inputbufferlength*は**sizeof**(WOF\_外部\_INFO) + **sizeof**(**WIM\_PROVIDER\_UPDATE\_オーバーレイ\_入力**) になります。 **Wim\_PROVIDER\_UPDATE\_オーバーレイ**の**DataSourceId**値は、 [**FSCTL\_オーバーレイ**](fsctl-add-overlay.md)要求の追加で以前に追加された wim ファイルの\_入力である必要があります。

その他のバッキングプロバイダーは、独自の特定の入力パラメーター構造を定義します。

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
<td align="left"><p>Windows 8.1 更新プログラムから使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs (Ntifs または Fltkernel .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FSCTL\_\_オーバーレイの追加**](fsctl-add-overlay.md)

[**FSCTL\_\_オーバーレイの削除**](fsctl-remove-overlay.md)

[**FSCTL\_SUSPEND\_オーバーレイ**](fsctl-suspend-overlay.md)

[**FSCTL\_外部\_バッキング\_取得する**](fsctl-get-external-backing.md)

[**外部\_バッキング\_FSCTL\_設定**](fsctl-set-external-backing.md)

 

 






