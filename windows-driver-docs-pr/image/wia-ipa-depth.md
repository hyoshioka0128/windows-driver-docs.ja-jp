---
title: WIA\_IPA\_深さ
description: WIA\_IPA\_DEPTH プロパティには、イメージのビット深さの設定が含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 90f7983c-296f-4dfc-90d3-886881a907af
keywords:
- WIA_IPA_DEPTH イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPA_DEPTH
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd89ae491a066af635f902ee973b864c98c86300
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369549"
---
# <a name="wiaipadepth"></a>WIA\_IPA\_深さ


WIA\_IPA\_DEPTH プロパティには、イメージのビット深さの設定が含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。




プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

アプリケーションの読み取り、WIA\_IPA\_DEPTH プロパティ イメージのビット深度設定を確認します。 必要なビット深度、または、WIA アプリケーション、このプロパティ設定も\_深さ\_自動値。

デバイスを 1 つの値に設定すると作成、WIA\_PROP\_リストの種類と、有効な値を配置します。

WIA\_深さ\_(1 ピクセルあたりのビットを 0 として定義されている) 自動値は、ベッドとフィーダーを含むすべてプログラミング可能なイメージのデータ ソース項目に対して無効です。 WIA ミニ ドライバー、WIA アプリケーション クライアントがこの値がサポートされている場合、設定できる**WIA\_IPA\_深さ**デバイスでの色の自動検出を有効にするには、この値にします。

ときに、 **WIA\_IPA\_深さ**プロパティが WIA\_深さ\_AUTO、WIA ミニ ドライバーを更新する必要があります、 [ **WIA\_IPA\_DATATYPE** ](wia-ipa-datatype.md) WIA に同じ項目をプロパティ\_データ\_自動 (これは、デバイスは、自動の色をサポートしている場合は、サポートされている値をある必要があります)。 ときに、 **WIA\_IPA\_DATATYPE** WIA を値\_データ\_自動がサポートされている、 **WIA\_IPA\_深さ**値WIA\_深さ\_自動が省略可能なされなくなり、必要な値になります。

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
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





