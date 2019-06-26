---
title: WIA\_IP\_マルチ\_フィード
description: WIA\_IP\_マルチ\_フィードのプロパティを使用して、デバイスに複数のフィードの条件が検出されたときに、WIA ミニドライバーに行うアクションを構成します。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 8BD92273-218B-4381-BCAF-ED9D227B6B94
keywords:
- WIA_IPS_MULTI_FEED イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_MULTI_FEED
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8a32153e32c3341324042179e5bb40e5bf16428
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385309"
---
# <a name="wiaipsmultifeed"></a>WIA\_IP\_マルチ\_フィード


**WIA\_IP\_マルチ\_フィード**プロパティを使用して、デバイスに複数のフィードの条件が検出されたときに、WIA ミニドライバーに行うアクションを構成します。 WIA ミニドライバーは、作成し、このプロパティを保持します。




プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:[読み取り/書き込み]

<a name="remarks"></a>注釈
-------

次の表に、有効な値、 **WIA\_IP\_マルチ\_フィード**プロパティ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_MULTI_FEED_DETECT_DISABLED</p></td>
<td><p>複数のフィードの検出を無効にします。 これは、プロパティがサポートされている場合に必要な既定値です。</p></td>
</tr>
<tr class="even">
<td><p>WIA_MULTI_FEED_DETECT_STOP_ERROR</p></td>
<td><p>デバイスが複数のフィードを検出し、スキャンが停止、MULTIPLE_FEED のビットを設定<a href="wia-dps-document-handling-status.md" data-raw-source="[&lt;strong&gt;WIA_DPS_DOCUMENT_HANDLING_STATUS&lt;/strong&gt;](wia-dps-document-handling-status.md)"> <strong>WIA_DPS_DOCUMENT_HANDLING_STATUS</strong></a>、WIA_ERROR_MULTI_FEED に戻って<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvAcquireItemData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)"> <strong>IWiaMiniDrv::drvAcquireItemData</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_MULTI_FEED_DETECT_STOP_SUCCESS</p></td>
<td><p>デバイスが複数のフィードを検出し、スキャンが停止、MULTIPLE_FEED のビットを設定<a href="wia-dps-document-handling-status.md" data-raw-source="[&lt;strong&gt;WIA_DPS_DOCUMENT_HANDLING_STATUS&lt;/strong&gt;](wia-dps-document-handling-status.md)"> <strong>WIA_DPS_DOCUMENT_HANDLING_STATUS</strong></a>、および<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvAcquireItemData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)"> <strong>IWiaMiniDrv::drvAcquireItemData</strong> </a>返しため、複数のフィードは失敗しません。</p></td>
</tr>
<tr class="even">
<td><p>WIA_MULTI_FEED_DETECT_CONTINUE</p></td>
<td><p>デバイスで複数のフィードを検出または警告音を鳴らす (お勧めしますが、必要ありません) は、ハードウェア デバイスでの音声または画面信号が生成されます、スキャンが続行されます。</p></td>
</tr>
</tbody>
</table>

 

このプロパティは省略可能で、フィーダー付きのデータ ソース アイテムにのみ有効です (で表される、 [ **WIA\_IPA\_項目\_カテゴリ**](wia-ipa-item-category.md)として WIAプロパティ\_カテゴリ\_フィーダー)。

WIA ミニドライバーが、複数を設定するときに\_フィードのビットを[ **WIA\_DPS\_ドキュメント\_処理\_状態**](wia-dps-document-handling-status.md)プロパティ間もなく、ミニドライバーは、フィーダーがアンロードされての再読み込みが検出されると、新しいスキャン ジョブの開始時、ミニドライバーこのビット (フラグ) をオフにする必要があります。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





