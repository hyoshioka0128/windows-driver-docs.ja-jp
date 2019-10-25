---
title: WIA\_IP\_フィーダー\_コントロール
description: WIA\_IP\_フィーダー\_コントロールのプロパティを使用して、フィーダーモーターの手動制御を構成します。 このプロパティは、WIA ミニドライバーによって作成および管理されます。
ms.assetid: CA19D573-B461-4D3E-BE2A-CF350E0FA4EA
keywords:
- WIA_IPS_FEEDER_CONTROL イメージングデバイス
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
ms.openlocfilehash: 90823a2c6d171dd154218dac43ea96eb15ee30b1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840688"
---
# <a name="wia_ips_feeder_control"></a>WIA\_IP\_フィーダー\_コントロール


**WIA\_ip\_フィーダー\_コントロール**のプロパティを使用して、フィーダーモーターの手動制御を構成します。 このプロパティは、WIA ミニドライバーによって作成および管理されます。




プロパティの型: VT\_I4

有効な値: WIA\_PROP\_LIST

アクセス権: 読み取り/書き込み

<a name="remarks"></a>注釈
-------

次の表では、 **WIA\_ip\_フィーダー\_コントロール**プロパティの有効な値について説明します。

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
<td><p>デバイスは、フィーダーモーター操作を制御します。 各スキャンジョブ (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvAcquireItemData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)"><strong>IWiaMiniDrv::D rvacquireitemdata</strong></a>呼び出し) でフィーダーが開始され、停止します。 これは、プロパティがサポートされている場合に必要な既定値です。</p></td>
</tr>
<tr class="even">
<td><p>WIA_FEEDER_CONTROL_MANUAL</p></td>
<td><p>アプリケーションは、フィーダーモーターの操作を制御します。 このフィーダーは、WIA ミニドライバーが WIA_COMMAND_START_FEEDER コマンド要求を受信したときに開始され、WIA ミニドライバーが WIA_COMMAND_STOP_FEEDER コマンド要求を受信すると停止します。</p></td>
</tr>
</tbody>
</table>

 

デバイスでこの機能がサポートされている場合、WIA アプリケーションでは、最初のスキャンジョブ (最初の**IWiaTransfer::D o)** 呼び出し) を実行する前に、それを使用してフィーダーモータを起動し、最後のスキャンジョブの後にフィーダーを停止します (最後の**IWiaTransfer::D o)** 現在の WIA アプリケーションセッションの呼び出しが完了しました)。 個々のジョブ (**IWiaTransfer::D o)** 呼び出し) の間には、フィーダーの動作速度が維持され、次のジョブを遅延なしで続行できます。

Wia ミニドライバーが[**IWiaMiniDrv::D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)要求を受信しているときに、WIA\_フィーダー\_制御\_手動が設定されていて、WIA\_コマンドを受け取らない場合は、wia\_スキャンジョブを実行する前に、ミニドライバーは WIA\_フィーダー\_コマンド\_自動に戻す必要があります。

WIA\_フィーダー\_CONTROL\_MANUAL が設定されている場合、wia ミニドライバーは、WIA\_コマンドを受信せずに[**IWiaMiniDrv::D rvuninitializewia**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvuninitializewia)要求を受信すると、wia ミニドライバーは、呼び出しに戻る前に、フィーダーを停止します。

このプロパティは、フィーダー項目 (WIA\_カテゴリ\_フィーダー) に対してのみ有効であり、省略可能です。

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

 

 





