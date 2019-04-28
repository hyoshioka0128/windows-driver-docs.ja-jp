---
title: KSCATEGORY_TOPOLOGY
description: KSCATEGORY_TOPOLOGY
ms.assetid: 20c4ccf1-81bb-4209-9842-4de295fe3a00
keywords:
- KSCATEGORY_TOPOLOGY デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_TOPOLOGY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 15c8ca4c096ac71383e0b68ca59c674700cc8e55
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361152"
---
# <a name="kscategorytopology"></a>KSCATEGORY_TOPOLOGY


KSCATEGORY_TOPOLOGY[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff568277)(KS) オーディオ デバイスの内部のトポロジの機能のカテゴリ。

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
<td align="left"><p>KSCATEGORY_TOPOLOGY</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{DDA54A40-1E4C-11D1-A050-405705C10000}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KS オーディオ アダプター デバイス用のドライバーでは、オペレーティング システムに、デバイスが KSCATEGORY_TOPOLOGY 機能カテゴリをサポートすることを示す KSCATEGORY_TOPOLOGY のインスタンスを登録します。

オーディオのアダプターのインターフェイス クラスのデバイスについては、次を参照してください。[オーディオのアダプターのデバイスのインターフェイスをインストールする](https://msdn.microsoft.com/library/windows/hardware/ff536813)します。

[AC'97 サンプル ドライバー](https://go.microsoft.com/fwlink/p/?linkid=256075)で提供されている、WDK KSCATEGORY_TOPOLOGY デバイス インターフェイス クラスのインスタンスを列挙します。

WDK の sysfx サンプルでは、このデバイスのインターフェイス クラスのインスタンスを登録します。 Sysfx サンプルが記載されています、 *src\\オーディオ\\sysfx ディレクトリ*WDK の。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

 

 





