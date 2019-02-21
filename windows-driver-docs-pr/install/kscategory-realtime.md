---
title: KSCATEGORY_REALTIME
description: KSCATEGORY_REALTIME
ms.assetid: c9b0a31a-50d9-47bc-9345-5d73a95238c3
keywords:
- KSCATEGORY_REALTIME デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_REALTIME
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7e271ad074da413c9702a45bda559d342ae8c03e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550508"
---
# <a name="kscategoryrealtime"></a>KSCATEGORY_REALTIME


KSCATEGORY_REALTIME[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff568277)(KS) およびシステム バス (たとえば、PCI バス) に接続されている、オーディオ デバイスの機能のカテゴリ再生またはリアルタイムで wave データをキャプチャします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>識別子</p></td>
<td align="left"><p>KSCATEGORY_REALTIME</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{EB115FFC-10C8-4964-831D-6DCB02E6F23F}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KS デバイス用のドライバーでは、オペレーティング システムに、デバイスが KSCATEGORY_REALTIME 機能カテゴリをサポートすることを示す KSCATEGORY_REALTIME のインスタンスを登録します。

この機能のカテゴリを登録するデバイスは、システム提供によって運営されて[WaveRT ポート ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff538837)します。

INF ファイルでこの機能のカテゴリを登録する方法については、INF ファイルを参照してください。 *Ac97smpl.inf*に含まれる、 [AC'97 サンプル ドライバー](https://go.microsoft.com/fwlink/p/?linkid=256075) WDK に含まれています。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows Vista および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

 

 





