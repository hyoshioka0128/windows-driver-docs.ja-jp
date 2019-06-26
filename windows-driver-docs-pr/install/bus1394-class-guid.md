---
title: BUS1394_CLASS_GUID
description: BUS1394_CLASS_GUID
ms.assetid: 5452c829-b1d2-4a15-93ef-3d82ac6c04d0
keywords:
- BUS1394_CLASS_GUID デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- BUS1394_CLASS_GUID
api_location:
- 1394.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 36bfe1ceb2ac5e162e4bebfb24bb6002ad0caae2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386039"
---
# <a name="bus1394classguid"></a>BUS1394_CLASS_GUID


BUS1394_CLASS_GUID[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている[1394 バス デバイス](https://docs.microsoft.com/windows-hardware/drivers/ieee)します。

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
<td align="left"><p>BUS1394_CLASS_GUID</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{6BDD1FC1-810F-11d0-BEC7-08002BE2092F}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

1394 のバスのバス ドライバーでは、オペレーティング システムと 1394 bus デバイスの存在をアプリケーションに通知するこのデバイスのインターフェイス クラスのインスタンスを登録します。

1394 バスについては、次を参照してください。 [1394 バス デバイス](https://docs.microsoft.com/windows-hardware/drivers/ieee)します。

WDK サンプルに含まれて、 [1394api サンプル](https://docs.microsoft.com/windows-hardware/drivers/ieee/1394-samples-and-diagnostic-tools)アプリケーション。 このアプリケーションでは、BUS1394_CLASS_GUID を使用して、このデバイスのインターフェイス クラスのインスタンスの存在の通知に登録します。

IEEE 1394 デバイスに対するデバイスのインターフェイス クラスについては、61883[デバイス セットアップ クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)IEC 61883 プロトコルをサポートするを参照してください[ **GUID_61883_CLASS**](guid-61883-class.md)します。

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
<td align="left"><p>Windows XP および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">1394.h (1394.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**GUID_61883_CLASS**](guid-61883-class.md)

 

 






