---
title: WIA\_DPC\_フォーカス\_メータリング\_モード
description: WIA\_DPC\_フォーカス\_メータリング\_モード プロパティは、カメラを使用して、フォーカスを自動的に調整するモードを指定します。
ms.assetid: a6a45f46-504b-4dad-a292-496f1ea4d8a0
keywords:
- WIA_DPC_FOCUS_METERING_MODE イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPC_FOCUS_METERING_MODE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 954f8fd5abde30ba371549da7189e0a62e7b18d3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549565"
---
# <a name="wiadpcfocusmeteringmode"></a>WIA\_DPC\_フォーカス\_メータリング\_モード


WIA\_DPC\_フォーカス\_メータリング\_モード プロパティは、カメラを使用して、フォーカスを自動的に調整するモードを指定します。

## <span id="ddk_wia_dpc_focus_metering_mode_si"></span><span id="DDK_WIA_DPC_FOCUS_METERING_MODE_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

次の表は、WIA で有効な定数\_DPC\_フォーカス\_メータリング\_モード プロパティです。

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
<td><p>FOCUSMETERING_CENTERSPOT</p></td>
<td><p>中央の場所に基づいて、フォーカスを調整します。</p></td>
</tr>
<tr class="even">
<td><p>FOCUSMETERING_MULTISPOT</p></td>
<td><p>Multispot パターンに基づいて、フォーカスを調整します。</p></td>
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

 

 





