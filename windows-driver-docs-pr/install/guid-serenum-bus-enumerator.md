---
title: GUID_SERENUM_BUS_ENUMERATOR
description: GUID_SERENUM_BUS_ENUMERATOR
ms.assetid: 85d72641-e86c-4611-9509-aea4a3344950
keywords:
- GUID_SERENUM_BUS_ENUMERATOR デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_SERENUM_BUS_ENUMERATOR
api_location:
- Ntddser.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1b33951e0f97be7fd3f0e380c70b6b573d4d76e5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384781"
---
# <a name="guidserenumbusenumerator"></a>GUID_SERENUM_BUS_ENUMERATOR


GUID_SERENUM_BUS_ENUMERATOR は古い形式の識別子、[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)プラグ アンド プレイ (PnP) のシリアル ポート。 Microsoft Windows 2000 以降を使用して、 [ **GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR** ](guid-devinterface-serenum-bus-enumerator.md)このクラスの新しいインスタンスのクラス識別子。

<a name="remarks"></a>注釈
-------

WDK には、シリアル列挙子のサンプルが用意されています ([*serenum*](https://docs.microsoft.com/previous-versions/ff546505(v=vs.85)))。 シリアルの列挙子では、GUID_SERENUM_BUS_ENUMERATOR を使用して、このデバイスのインターフェイス クラスのインスタンスを登録します。 含まれている serenum サンプル、 *src\\カーネル*WDK のディレクトリ。

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
<td align="left"><p>使われていません。 Windows 2000 以降、GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR を代わりに使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntddser.h (Ntddser.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR**](guid-devinterface-serenum-bus-enumerator.md)

 

 






