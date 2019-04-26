---
title: WIA\_IP\_LAMP\_自動\_OFF
description: WIA\_IP\_LAMP\_自動\_プロパティをオフには、スキャナーの lamp を自動的にシャット ダウンの現在の構成設定を格納します。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 82a3b5dc-0a70-4e2a-a863-6019b04cbbaf
keywords:
- WIA_IPS_LAMP_AUTO_OFF イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_LAMP_AUTO_OFF
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d296fb17bee8a6948a39815629aa882801c84666
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348336"
---
# <a name="wiaipslampautooff"></a>WIA\_IP\_LAMP\_自動\_OFF


WIA\_IP\_LAMP\_自動\_プロパティをオフには、スキャナーの lamp を自動的にシャット ダウンの現在の構成設定を格納します。 WIA ミニドライバーは、作成し、このプロパティを保持します。

プロパティの種類:VT\_UI4

有効な値 :WIA\_PROP\_範囲

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

WIA\_IP\_LAMP\_自動\_プロパティの有効無効、どれくらいの時間の lamp のプログラムによる制御は保持されますスキャナーが使用されていないときに; (透明度アダプター) の専用 lamp またはメインこの lamp 可能性があります(専用のフィルム スキャナー) に lamp をスキャナーです。

WIA を実装する必要があります\_IP\_LAMP\_自動\_デバイスは、自動のランプ オフ機能をサポートしている場合にのみオフします。

WIA の有効な値\_IP\_LAMP\_自動\_範囲 0 ~ 4095 秒オフします。

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
<td><p>Windows Vista およびそれ以降のオペレーティング システムで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





