---
title: WIA\_DPC\_画像\_残り
description: WIA\_DPC\_画像\_残りのプロパティには、ユーザーがデバイスを使用して、カメラ、プロパティの現在の設定を指定された実行できる画像の数が含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: ac6cd3e0-c6fe-4783-8094-67083e308308
keywords:
- WIA_DPC_PICTURES_REMAINING イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPC_PICTURES_REMAINING
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92dc180099c5f358bc1ae852b31c8b4ebd9cbf31
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379588"
---
# <a name="wiadpcpicturesremaining"></a>WIA\_DPC\_画像\_残り


WIA\_DPC\_画像\_残りのプロパティには、ユーザーがデバイスを使用して、カメラ、プロパティの現在の設定を指定された実行できる画像の数が含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。

## <span id="ddk_wia_dpc_pictures_remaining_si"></span><span id="DDK_WIA_DPC_PICTURES_REMAINING_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

場合、WIA\_DPC\_画像\_カメラ デバイスを生成するイメージのサイズに影響する残りのプロパティの設定の変更と、変更、WIA ミニドライバーは、残りの画像の数を更新する必要があります。

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

 

 





