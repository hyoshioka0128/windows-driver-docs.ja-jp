---
title: WIA\_DPC\_キャプチャ\_モード
description: WIA\_DPC\_キャプチャ\_モード プロパティは、イメージのキャプチャ モードを設定します。
ms.assetid: 32d117ac-fa20-49cc-a34e-31a1be88804e
keywords:
- WIA_DPC_CAPTURE_MODE イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPC_CAPTURE_MODE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad79d73dc648069fc20b38e39f9bc09f32f8cb1e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342785"
---
# <a name="wiadpccapturemode"></a>WIA\_DPC\_キャプチャ\_モード


WIA\_DPC\_キャプチャ\_モード プロパティは、イメージのキャプチャ モードを設定します。

## <span id="ddk_wia_dpc_capture_mode_si"></span><span id="DDK_WIA_DPC_CAPTURE_MODE_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

次の表に、3 つの定数、WIA で有効な\_DPC\_キャプチャ\_モード プロパティです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>値</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CAPTUREMODE_BURST</p></td>
<td><p>値で定義されている立て続けに 2 つ以上のイメージをキャプチャ、 <a href="wia-dpc-burst-number.md" data-raw-source="[&lt;strong&gt;WIA_DPC_BURST_NUMBER&lt;/strong&gt;](wia-dpc-burst-number.md)"> <strong>WIA_DPC_BURST_NUMBER</strong> </a>と<a href="wia-dpc-burst-interval.md" data-raw-source="[&lt;strong&gt;WIA_DPC_BURST_INTERVAL&lt;/strong&gt;](wia-dpc-burst-interval.md)"> <strong>WIA_DPC_BURST_INTERVAL</strong> </a>プロパティ。</p></td>
</tr>
<tr class="even">
<td><p>CAPTUREMODE_NORMAL</p></td>
<td><p>カメラの通常のモードです。</p></td>
</tr>
<tr class="odd">
<td><p>CAPTUREMODE_TIMELAPSE</p></td>
<td><p>定義されている、連続して 2 つ以上のイメージをキャプチャ、 <a href="wia-dpc-timelapse-number.md" data-raw-source="[&lt;strong&gt;WIA_DPC_TIMELAPSE_NUMBER&lt;/strong&gt;](wia-dpc-timelapse-number.md)"> <strong>WIA_DPC_TIMELAPSE_NUMBER</strong> </a>と<a href="wia-dpc-timelapse-interval.md" data-raw-source="[&lt;strong&gt;WIA_DPC_TIMELAPSE_INTERVAL&lt;/strong&gt;](wia-dpc-timelapse-interval.md)"> <strong>WIA_DPC_TIMELAPSE_INTERVAL</strong> </a>プロパティ。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista 以降のオペレーティング システムで古いものであり使用できなくする必要があります。 ただし、アプリケーションやデバイス向けの Windows Server 2003、Windows XP、および Windows の以前のバージョンと互換性のこのプロパティが現在も Windows Vista で定義します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_DPC\_バースト\_間隔**](wia-dpc-burst-interval.md)

[**WIA\_DPC\_バースト\_数**](wia-dpc-burst-number.md)

[**WIA\_DPC\_TIMELAPSE\_間隔**](wia-dpc-timelapse-interval.md)

[**WIA\_DPC\_TIMELAPSE\_数**](wia-dpc-timelapse-number.md)

 

 






