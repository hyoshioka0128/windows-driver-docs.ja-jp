---
title: KSCATEGORY_ENCODER
description: KSCATEGORY_ENCODER
ms.assetid: 409dbb1f-7b28-4cb3-bdba-da927cf67133
keywords:
- KSCATEGORY_ENCODER デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_ENCODER
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1c46404759531fd809ee04b6625891b2b611debe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365839"
---
# <a name="kscategoryencoder"></a>KSCATEGORY_ENCODER


KSCATEGORY_ENCODER[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff568277)データ エンコード (KS) 機能のカテゴリ。

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
<td align="left"><p>KSCATEGORY_ENCODER</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{19689BF6-C384-48fd-AD51-90E58C79F70B}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

KS デバイス用のドライバーでは、オペレーティング システムに、デバイスが KSCATEGORY_ENCODER 機能カテゴリをサポートすることを示す KSCATEGORY_ENCODER のインスタンスを登録します。

INF ファイルでこの機能のカテゴリを登録する方法の例は、次を参照してください。、 *Bdan.inf* INF ファイルでのソフトウェアのチューナー サンプルに含まれている、 *src/swtuner/algtuner* WDK のディレクトリ。

エンコーダーの詳細については、次を参照してください。[エンコーダー デバイス](https://msdn.microsoft.com/library/windows/hardware/ff559535)と[エンコーダーのインストールと登録](https://msdn.microsoft.com/library/windows/hardware/ff559551)します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows Vista、Windows Server 2003、Windows XP Service Pack 1 (SP1)、および以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

 

 





