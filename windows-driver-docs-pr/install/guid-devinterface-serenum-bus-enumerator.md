---
title: GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR
description: GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR
ms.assetid: 163b58b1-9f88-4857-9899-32be5e9ffc3c
keywords:
- GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR
api_location:
- Ntddser.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 28fe9fdcd40a5035dee434b737f385f5237e25b3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386427"
---
# <a name="guiddevinterfaceserenumbusenumerator"></a>GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR


GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)プラグ アンド プレイ (PnP) が定義されている[シリアル ポート](https://docs.microsoft.com/previous-versions/ff547451(v=vs.85))します。

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
<td align="left"><p>GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{4D36E978-E325-11CE-BFC1-08002BE10318}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

デバイスのシリアル ポートのシステム指定の列挙子は、オペレーティング システムとデバイスのシリアル ポートの存在をアプリケーションに通知する GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR のインスタンスを登録します。

WDK には、シリアル列挙子のサンプルが含まれています。 [serenum](https://docs.microsoft.com/previous-versions/ff546505(v=vs.85))します。 Serenum サンプルが古い形式の識別子を使用して[ **GUID_SERENUM_BUS_ENUMERATOR** ](guid-serenum-bus-enumerator.md)をこのデバイスのインターフェイス クラスのインスタンスを登録します。 Serenum サンプルが記載されています、 *src\\カーネル*WDK のディレクトリ。

シリアル デバイスとドライバーについては、次を参照してください。[シリアル デバイスとドライバー](https://docs.microsoft.com/previous-versions/ff547451(v=vs.85))します。

シリアル ポートのデバイスに対するデバイスのインターフェイス クラスについては、次を参照してください。 [ **GUID_DEVINTERFACE_COMPORT**](guid-devinterface-comport.md)します。

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
<td align="left">Ntddser.h (Ntddser.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**GUID_DEVINTERFACE_COMPORT**](guid-devinterface-comport.md)

[**GUID_SERENUM_BUS_ENUMERATOR**](guid-serenum-bus-enumerator.md)

 

 






