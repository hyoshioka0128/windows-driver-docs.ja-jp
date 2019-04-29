---
title: WIA\_DPC\_効果\_モード
description: WIA\_DPC\_効果\_モード プロパティは、カメラの特別なイメージの取得モードを指定します。
ms.assetid: a874858d-4400-425f-8423-b41bbeb1a925
keywords:
- WIA_DPC_EFFECT_MODE イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPC_EFFECT_MODE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f1020b54e82117137b318ce86b9a3787aeaa448
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373109"
---
# <a name="wiadpceffectmode"></a>WIA\_DPC\_効果\_モード


WIA\_DPC\_効果\_モード プロパティは、カメラの特別なイメージの取得モードを指定します。

## <span id="ddk_wia_dpc_effect_mode_si"></span><span id="DDK_WIA_DPC_EFFECT_MODE_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

次の表は、WIA で有効な定数\_DPC\_効果\_モード プロパティです。

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
<td><p>EFECTMODE_BW</p></td>
<td><p>グレースケール イメージをキャプチャします。</p></td>
</tr>
<tr class="even">
<td><p>EFFECTMODE_SEPIA</p></td>
<td><p>セピア イメージをキャプチャします。</p></td>
</tr>
<tr class="odd">
<td><p>EFFECTMODE_STANDARD</p></td>
<td><p>カメラの標準モードでイメージをキャプチャします。</p></td>
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

 

 





