---
title: GUID_DEVINTERFACE_COMPORT
description: GUID_DEVINTERFACE_COMPORT
ms.assetid: ce7fbe64-1445-4702-898e-2fc92f96ebf9
keywords:
- GUID_DEVINTERFACE_COMPORT デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_COMPORT
api_location:
- Ntddser.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9b92f88c737d337ff710341cfe3c4a7ea19ff336
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372739"
---
# <a name="guiddevinterfacecomport"></a>GUID_DEVINTERFACE_COMPORT


GUID_DEVINTERFACE_COMPORT[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている[COM ポート](https://docs.microsoft.com/previous-versions/ff546485(v=vs.85))します。

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
<td align="left"><p>GUID_DEVINTERFACE_COMPORT</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{86E0D1E0-8089-11D0-9CE4-08003E301F73}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

シリアル ポート用のドライバーでは、オペレーティング システムとアプリケーションの COM ポートの存在を通知するこのデバイスのインターフェイス クラスのインスタンスを登録します。

シリアル ポートのシステムによって提供される関数ドライバーに対するこのデバイスのインターフェイス クラスのインスタンスに登録する[シリアル ポート](https://docs.microsoft.com/previous-versions/ff547451(v=vs.85))します。

次のサンプル (Github 上) は、シリアル ポートには、このクラスのインスタンスを登録します。

-   [シリアル サンプル](https://go.microsoft.com/fwlink/p/?LinkId=617962)
-   [仮想シリアル ドライバーのサンプル](https://go.microsoft.com/fwlink/p/?LinkId=617963)(UMDF 1.0)
-   [仮想 serial2 ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=722209)(KMDF)

[**GUID_CLASS_COMPORT** ](guid-class-comport.md)このデバイス インターフェイス クラスの古い形式の識別子は、このクラスの新しいインスタンスが GUID_DEVINTERFACE_COMPORT を代わりに使用します。

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
<td align="left"><p>Microsoft Windows 2000 および以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntddser.h (Ntddser.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**GUID_CLASS_COMPORT**](guid-class-comport.md)

 

 






