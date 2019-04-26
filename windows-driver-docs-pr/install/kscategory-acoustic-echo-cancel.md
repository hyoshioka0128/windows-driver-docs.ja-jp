---
title: KSCATEGORY_ACOUSTIC_ECHO_CANCEL
description: KSCATEGORY_ACOUSTIC_ECHO_CANCEL
ms.assetid: 91440365-be16-4d98-aa91-e186b9ab6359
keywords:
- KSCATEGORY_ACOUSTIC_ECHO_CANCEL デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_ACOUSTIC_ECHO_CANCEL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ecde56415d4c1f5266057adf38a4177105fbcf5d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342726"
---
# <a name="kscategoryacousticechocancel"></a>KSCATEGORY_ACOUSTIC_ECHO_CANCEL


KSCATEGORY_ACOUSTIC_ECHO_CANCEL[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff568277)アコースティック エコー キャンセルを実行します (KS) 機能のカテゴリ。

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
<td align="left"><p>KSCATEGORY_ACOUSTIC_ECHO_CANCEL</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{BF963D80-C559-11D0-8A2B-00A0C9255AC1}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KS オーディオ デバイス用のドライバーでは、オペレーティング システムに、デバイスがアコースティック エコー キャンセルを実行する KS 機能のカテゴリをサポートすることを示す KSCATEGORY_ACOUSTIC_ECHO_CANCEL のインスタンスを登録します。

オーディオのアダプターのインターフェイス クラスのデバイスについては、次を参照してください。[オーディオのアダプターのデバイスのインターフェイスをインストールする](https://msdn.microsoft.com/library/windows/hardware/ff536813)します。

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

 

 





