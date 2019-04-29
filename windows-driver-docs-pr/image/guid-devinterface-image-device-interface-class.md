---
title: GUID\_DEVINTERFACE\_イメージ デバイス インターフェイス クラス
description: GUID\_DEVINTERFACE\_イメージ デバイス インターフェイス クラス
ms.assetid: 2bf0bb35-c047-481e-a0f3-b8a8c06e259b
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e8d00e84517b9e06f573a3b6ed32bb04e9d5aa4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330283"
---
# <a name="guiddevinterfaceimage-device-interface-class"></a>GUID\_DEVINTERFACE\_イメージ デバイス インターフェイス クラス


イメージ[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている[デバイスを静止画像](https://msdn.microsoft.com/library/windows/hardware/ff542729)デジタル カメラやスキャナーなど、します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>マニフェスト定数</p></td>
<td><p>GUID_DEVINTERFACE_IMAGE</p></td>
</tr>
<tr class="even">
<td><p>クラス GUID</p></td>
<td><p>{0x6bdd1fc6L、0x810f、0x11d0、0xbe、xc 0xc7、0x08、0x00、0x2b、0 xe2、0x09、0x2f}</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idheadersspanspan-idheadersspanheaders"></a><span id="headers"></span><span id="HEADERS"></span>ヘッダー

定義されている*Wiaintfc.h*します。 含める*Wiaintfc.h します。*

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

静止画像デバイス用のシステム提供のカーネル モード ドライバーでは、静止画像デバイスに対するこのデバイスのインターフェイス クラスのインスタンスを登録します。 このデバイスのインターフェイス クラスのインスタンスは、I/O インターフェイスのドライバー サポートを静止画像を使用してアクセスできます。 まだイメージのデバイスとドライバーの詳細については、次を参照してください。 [Windows Image Acquisition ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff553346)します。

このインターフェイスは、まだイメージのドライバーと WIA ドライバーに適用されますは、Microsoft Windows XP および Windows の以降のバージョンを使用できます。

 

 





