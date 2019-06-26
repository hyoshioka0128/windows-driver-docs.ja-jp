---
title: WIA\_IP\_フィーダー\_コントロール
description: WIA\_IP\_フィーダー\_フィーダー モーターを手動で制御を構成するコントロール プロパティを使用します。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: CA19D573-B461-4D3E-BE2A-CF350E0FA4EA
keywords:
- WIA_IPS_FEEDER_CONTROL イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_FEEDER_CONTROL
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0661a204e988c1c2eaa89ec53064742d977b0df
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372748"
---
# <a name="wiaipsfeedercontrol"></a>WIA\_IP\_フィーダー\_コントロール


**WIA\_IP\_フィーダー\_コントロール**フィーダー モーターを手動で制御を構成するプロパティを使用します。 WIA ミニドライバーは、作成し、このプロパティを保持します。




プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:[読み取り/書き込み]

<a name="remarks"></a>注釈
-------

次の表に、有効な値、 **WIA\_IP\_フィーダー\_コントロール**プロパティ。

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
<td><p>WIA_FEEDER_CONTROL_AUTO</p></td>
<td><p>デバイスは、フィーダー モーターの動作を制御します。 フィーダーが開始および各スキャン ジョブの停止 (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvAcquireItemData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)"><strong>IWiaMiniDrv::drvAcquireItemData</strong> </a>呼び出します)。 これは、プロパティがサポートされている場合に必要な既定値です。</p></td>
</tr>
<tr class="even">
<td><p>WIA_FEEDER_CONTROL_MANUAL</p></td>
<td><p>アプリケーションでは、フィーダー モーターの動作を制御します。 フィーダーが WIA ミニドライバー WIA_COMMAND_START_FEEDER コマンド要求を受信するときに開始し、WIA ミニドライバー WIA_COMMAND_STOP_FEEDER コマンド要求を受信する場合に停止します。</p></td>
</tr>
</tbody>
</table>

 

デバイスは、この機能をサポートするときに、WIA アプリケーションで使用フィーダー モーターを最初のスキャン ジョブを実行する前に開始する (最初の**IWiaTransfer::Download**呼び出し) と最後のスキャン ジョブの完了後、フィーダーを停止 (最終**IWiaTransfer::Download** WIA アプリケーションの現在のセッションで呼び出す) が完了します。 個々 のジョブの間で (**IWiaTransfer::Download**呼び出し)、フィーダーの処理速度に保持され、遅延なしに、次のジョブを続行する準備ができました。

WIA ミニドライバーを受信した場合、 [ **IWiaMiniDrv::drvAcquireItemData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata) WIA 中に要求\_フィーダー\_コントロール\_手動設定と、WIA がない場合は、\_コマンド\_開始\_フィーダー コマンド、WIA ミニドライバーは、WIA を元に戻す必要があります\_フィーダー\_コマンド\_自動スキャン ジョブを実行する前にします。

場合 WIA\_フィーダー\_コントロール\_手動に設定されているし、WIA ミニドライバーを受け取る、 [ **IWiaMiniDrv::drvUnInitializeWia** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvuninitializewia) WIAを受けることがなく要求\_コマンド\_停止\_フィーダー コマンド、WIA ミニドライバーは、呼び出しに戻る前に、フィーダーを停止する必要があります。

このプロパティは、フィーダー項目に対してのみ有効です (WIA\_カテゴリ\_フィーダー) は省略可能です。

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

 

 





