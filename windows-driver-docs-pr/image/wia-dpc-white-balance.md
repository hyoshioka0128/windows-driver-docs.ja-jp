---
title: WIA\_DPC\_白い\_のバランスを取る
description: WIA\_DPC\_白い\_残高プロパティは、デジタル カメラでのカラー チャネルをブレンドする方法を指定します。
ms.assetid: f0f9dd8e-940a-4a42-b6d7-1d1e86c0a530
keywords:
- WIA_DPC_WHITE_BALANCE イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPC_WHITE_BALANCE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c425bdf3aa283ebe95db37928ce9d4dff807c0ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527826"
---
# <a name="wiadpcwhitebalance"></a>WIA\_DPC\_白い\_のバランスを取る


WIA\_DPC\_白い\_残高プロパティは、デジタル カメラでのカラー チャネルをブレンドする方法を指定します。

## <span id="ddk_wia_dpc_white_balance_si"></span><span id="DDK_WIA_DPC_WHITE_BALANCE_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

次の表では、使用可能な値を示します、wia\_DPC\_白い\_残高プロパティ。

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
<td><p>WHITEBALANCE_AUTO</p></td>
<td><p>カメラでは、自動メカニズムを使用して、ホワイト バランスを設定します。</p></td>
</tr>
<tr class="even">
<td><p>WHITEBALANCE_DAYLIGHT</p></td>
<td><p>カメラでは、ホワイト バランスを夏時間条件で使用するための適切な値に設定します。</p></td>
</tr>
<tr class="odd">
<td><p>WHITEBALANCE_FLASH</p></td>
<td><p>カメラでは、ホワイト バランスを electronic flash で使用するための適切な値に設定します。</p></td>
</tr>
<tr class="even">
<td><p>WHITEBALANCE_FLORESCENT</p></td>
<td><p>カメラでは、ホワイト バランスを蛍光灯光源で使用するための適切な値に設定します。</p></td>
</tr>
<tr class="odd">
<td><p>WHITEBALANCE_MANUAL</p></td>
<td><p>ドライバーを使用して直接ホワイト バランスを設定することができます、 <a href="wia-dpc-rgb-gain.md" data-raw-source="[&lt;strong&gt;WIA_DPC_RGB_GAIN&lt;/strong&gt;](wia-dpc-rgb-gain.md)"> <strong>WIA_DPC_RGB_GAIN</strong> </a>プロパティ。</p></td>
</tr>
<tr class="even">
<td><p>WHITEBALANCE_ONEPUSH_AUTO</p></td>
<td><p>カメラは、ユーザーが白の画面でカメラをポイントした状態のキャプチャ ボタンを押したときに、ホワイト バランス設定を決定します。</p></td>
</tr>
<tr class="odd">
<td><p>WHITEBALANCE_TUNGSTEN</p></td>
<td><p>カメラでは、ホワイト バランスを tungsten 光源で使用するための適切な値に設定します。</p></td>
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


[**WIA\_DPC\_RGB\_を得る**](wia-dpc-rgb-gain.md)

 

 






