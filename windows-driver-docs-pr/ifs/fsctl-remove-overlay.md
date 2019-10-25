---
title: FSCTL_REMOVE_OVERLAY 制御コード
description: FSCTL\_REMOVE\_オーバーレイコントロールコードは、バッキングソースをボリュームから削除します。
ms.assetid: 9AB1DD06-AFB3-45AF-8139-14B60076D63A
keywords:
- FSCTL_REMOVE_OVERLAY 制御コードのインストール可能なファイルシステムドライバー
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
ms.openlocfilehash: bfec7a0997564edd8681bef5888414ff24da464d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841264"
---
# <a name="fsctl_remove_overlay-control-code"></a>FSCTL\_\_オーバーレイコントロールコードの削除


**FSCTL\_REMOVE\_オーバーレイ**コントロールコードは、バッキングソースをボリュームから削除します。

この操作を実行するには、次のパラメーターを使用して[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を呼び出します。

**パラメーター**

<a href="" id="instance--in-"></a> *\]のインスタンス \[*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 呼び出し元の非透過インスタンスポインター。 このパラメーターは必須であり、NULL にすることはできません。

<a href="" id="fileobject--in-"></a> *\]の FileObject \[*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 オーバーレイの削除元となるボリュームのファイルポインターオブジェクト。 このパラメーターは必須であり、NULL にすることはできません。

<a href="" id="filehandle--in-"></a> *\]の FileHandle \[*  
[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみ。 オーバーレイが削除されるボリュームのハンドル。 このパラメーターは必須であり、NULL にすることはできません。

<a href="" id="fscontrolcode--in-"></a> *\]の FsControlCode \[*  
操作の制御コード。 この操作には、FSCTL\_使用して **\_オーバーレイを削除**してください。

<a href="" id="inputbuffer"></a>*InputBuffer*  
入力バッファーへのポインター。これには、 [**WOF\_外部\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)構造体が含まれている必要があります。 必要に応じて、追加のプロバイダー固有のデータは、 **WOF\_外部\_情報**に含まれます。 プロバイダーが WIM ファイルの場合、 [**wim\_プロバイダー\_削除\_オーバーレイ\_入力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_remove_overlay_input)構造は、 **WOF\_外部\_情報**に含まれています。

<a href="" id="inputbufferlength--in-"></a> *\]内の InputBufferLength \[*  
**Sizeof**([**WOF\_外部\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)) に、追加のプロバイダー入力データのサイズを加えた値に設定します。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[out\]*  
使用されません。 NULL に設定されている。

<a href="" id="outputbufferlength--in-"></a> *\]の OutputBufferLength \[*  
を0に設定します。

<a name="status-block"></a>状態ブロック
------------

[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)は、操作が成功した場合に STATUS\_SUCCESS を返します。 それ以外の場合、適切な関数は、次のいずれかの NTSTATUS 値を返す可能性があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">期間</th>
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
<td align="left"><p><em>Outputbuffer</em>によってポイントされ、 <em>outputbufferlength</em>によって指定された出力バッファーの長さが小さすぎます。</p></td>
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

 

<a name="remarks"></a>解説
-------

削除するバッキングソースが Windows Imaging Format (WIM) ファイルの場合、入力バッファーには、 [**WOF\_外部\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wof_external_info)構造体の後に[**WIM\_\_プロバイダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_wim_provider_remove_overlay_input)が含まれます。これにより、オーバーレイ\_入力が削除されます。データ.\_ この場合、 *Inputbufferlength*は**sizeof**(WOF\_外部\_INFO) + **sizeof**(**WIM\_プロバイダー\_\_オーバーレイ\_入力**) を削除します。 Wim\_PROVIDER の**DataSourceId**値 **\_\_オーバーレイの削除\_入力**は、 [**FSCTL\_オーバーレイ**](fsctl-add-overlay.md)要求の追加で以前に追加された wim ファイルに対して行う必要があります。\_

追加のバッキングプロバイダーは、独自の特定の入力パラメーター構造を定義します。

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
<td align="left"><p>Windows 8.1 更新プログラムから使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ヘッダー</p></td>
<td align="left">Ntifs (Ntifs または Fltkernel .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FSCTL\_SUSPEND\_オーバーレイ**](fsctl-suspend-overlay.md)

[**FSCTL\_UPDATE\_オーバーレイ**](fsctl-update-overlay.md)

[**FSCTL\_外部\_バッキング\_取得する**](fsctl-get-external-backing.md)

[**外部\_バッキング\_FSCTL\_設定**](fsctl-set-external-backing.md)

 

 






