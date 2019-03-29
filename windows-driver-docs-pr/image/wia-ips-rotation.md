---
title: WIA\_IP\_回転
description: WIA\_IP\_ROTATION プロパティが実装されている場合、画像の回転の現在の回転設定には含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 5d117d55-b7e4-46eb-aeb5-54636749081f
keywords:
- WIA_IPS_ROTATION イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_ROTATION
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f2641acc7ce0367701a9759383d74babcfe4e0c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582110"
---
# <a name="wiaipsrotation"></a>WIA\_IP\_回転


WIA\_IP\_ROTATION プロパティが実装されている場合、画像の回転の現在の回転設定には含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。

## <span id="ddk_wia_ips_rotation_si"></span><span id="DDK_WIA_IPS_ROTATION_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>コメント
-------

アプリケーション設定、WIA\_IP\_ROTATION プロパティ ドライバーをどの程度 (すべての場合) に通知するために、ドライバーは、アプリケーションに返す前に画像を回転します。

次の表に、WIA に対して定義されている回転定数\_IP\_回転します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>定数</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>縦向き</p></td>
<td><p>ドライバーでは、イメージを回転はできません。</p></td>
</tr>
<tr class="even">
<td><p>LANSCAPE</p></td>
<td><p>ドライバーは、反時計回りに 90 度、イメージを回転します。</p></td>
</tr>
<tr class="odd">
<td><p>ROT180</p></td>
<td><p>ドライバーは、反時計回りに 180 度のイメージを回転します。</p></td>
</tr>
<tr class="even">
<td><p>ROT270</p></td>
<td><p>ドライバーは、反時計回りに 270 度のイメージを回転します。</p></td>
</tr>
</tbody>
</table>

 

WIA ミニドライバーは、アプリケーションに送信する前に画像データを交換します。 アプリケーションは、新しく回転値を表示するイメージのヘッダーをチェックします。

現在のイメージの選択領域の回転の影響を理解することは難しい (によって定義された、 [ **WIA\_IP\_XPOS**](wia-ips-xpos.md)、 [ **WIA\_IP\_YPOS**](wia-ips-ypos.md)、 [ **WIA\_IP\_XEXTENT**](wia-ips-xextent.md)、および[**WIA\_IP\_YEXTENT** ](wia-ips-yextent.md)プロパティ)。

*選択領域*からイメージを取得できませんが、物理スキャナーに、選択した領域を参照します。 WIA\_IP\_ROTATION プロパティは*いない*選択領域を変更します。 ドライバーは、WIA に従って反時計回りの回転を適用\_IP\_回転ドライバーには、適切な選択領域が取得された後のみです。 WIA\_IP\_回転*は*出力のイメージのサイズに影響するため、これらのディメンションは、結果のイメージのデータのヘッダーに反映する必要があります。

[**WIA\_IP\_YEXTENT** ](wia-ips-yextent.md)に関連しない[ **WIA\_IP\_向き**](wia-ips-orientation.md)します。 WIA\_IP\_スキャンの; とは異なり、WIA 方向に対してスキャンするドキュメントの向きに印刷の向き\_IP\_回転がイメージに適用する回転をについて説明しますスキャンした後。

WIA\_IP\_向きスキャンする領域に影響を与えることができます。 すべてのページ サイズが横と縦と WIA な変更からのイメージのエクステントの両方で使用可能な\_IP\_方向は、イメージをトリミングでした。 WIA\_IP\_回転イメージ エクステントには影響しませんし、スキャンするのには、ドキュメントの方向は関係ありません。

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

## <a name="see-also"></a>関連項目


[**WIA\_IP\_向き**](wia-ips-orientation.md)

[**WIA\_IP\_XEXTENT**](wia-ips-xextent.md)

[**WIA\_IP\_XPOS**](wia-ips-xpos.md)

[**WIA\_IP\_YEXTENT**](wia-ips-yextent.md)

[**WIA\_IP\_YPOS**](wia-ips-ypos.md)

 

 






