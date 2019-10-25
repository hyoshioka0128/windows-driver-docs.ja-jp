---
title: マルチ\_フィード\_WIA\_IP
description: 複数のフィード条件がデバイスで検出された場合に、WIA ミニドライバーによって実行されるアクションを構成するには、WIA\_IP\_マルチ\_フィードのプロパティを使用します。 このプロパティは、WIA ミニドライバーによって作成および管理されます。
ms.assetid: 8BD92273-218B-4381-BCAF-ED9D227B6B94
keywords:
- WIA_IPS_MULTI_FEED イメージングデバイス
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
ms.openlocfilehash: e19f602adf098c3f018b2872d52b245381565fe7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840686"
---
# <a name="wia_ips_multi_feed"></a>マルチ\_フィード\_WIA\_IP


複数のフィード条件がデバイスで検出された場合に、WIA ミニドライバーによって実行されるアクションを構成するには、 **wia\_ip\_マルチ\_フィード**のプロパティを使用します。 このプロパティは、WIA ミニドライバーによって作成および管理されます。




プロパティの型: VT\_I4

有効な値: WIA\_PROP\_LIST

アクセス権: 読み取り/書き込み

<a name="remarks"></a>注釈
-------

次の表では、 **WIA\_ip\_マルチ\_フィード**のプロパティの有効な値について説明します。

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
<td><p>マルチフィード検出が無効になっています。 これは、プロパティがサポートされている場合に必要な既定値です。</p></td>
</tr>
<tr class="even">
<td><p>WIA_MULTI_FEED_DETECT_STOP_ERROR</p></td>
<td><p>デバイスはマルチフィードを検出し、スキャンを停止して、 <a href="wia-dps-document-handling-status.md" data-raw-source="[&lt;strong&gt;WIA_DPS_DOCUMENT_HANDLING_STATUS&lt;/strong&gt;](wia-dps-document-handling-status.md)"><strong>WIA_DPS_DOCUMENT_HANDLING_STATUS</strong></a>の MULTIPLE_FEED ビットを設定し、WIA_ERROR_MULTI_FEED を<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvAcquireItemData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)"><strong>IWiaMiniDrv::d rvacquireitemdata</strong></a>に返します。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_MULTI_FEED_DETECT_STOP_SUCCESS</p></td>
<td><p>デバイスは、マルチフィードを検出し、スキャンを停止し、 <a href="wia-dps-document-handling-status.md" data-raw-source="[&lt;strong&gt;WIA_DPS_DOCUMENT_HANDLING_STATUS&lt;/strong&gt;](wia-dps-document-handling-status.md)"><strong>WIA_DPS_DOCUMENT_HANDLING_STATUS</strong></a>の MULTIPLE_FEED ビットを設定します。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvAcquireItemData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)"><strong>IWiaMiniDrv::d rvacquireitemdata</strong></a>は、マルチフィードのために失敗しません。</p></td>
</tr>
<tr class="even">
<td><p>WIA_MULTI_FEED_DETECT_CONTINUE</p></td>
<td><p>デバイスは、マルチフィード、ビープ音を検出するか、ハードウェアデバイスで可聴または表示信号を生成します (推奨されますが必須ではありません)。スキャンを続行します。</p></td>
</tr>
</tbody>
</table>

 

このプロパティは省略可能で、Wia データソース項目に対してのみ有効です (wia [ **\_IPA\_item\_category**](wia-ipa-item-category.md)プロパティは WIA\_CATEGORY\_フィーダーとして表示されます)。

WIA ミニドライバーが[ **\_DPS\_ドキュメント\_\_STATUS**](wia-dps-document-handling-status.md)プロパティの複数の\_フィードビットを設定すると、ミニドライバーがフィーダーを認識していることを検出するとすぐに、ミニドライバーはこのビット (フラグ) をクリアする必要があります。アンロードされるか、再読み込みされるか、新しいスキャンジョブが開始されます。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef (Wiadef を含む)</td>
</tr>
</tbody>
</table>

 

 





