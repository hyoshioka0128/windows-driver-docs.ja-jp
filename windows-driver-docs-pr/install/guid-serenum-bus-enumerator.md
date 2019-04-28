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
ms.openlocfilehash: b5917d46e84dd6daa2b44be80eb131226c77fab4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369970"
---
# <a name="guidserenumbusenumerator"></a>GUID_SERENUM_BUS_ENUMERATOR


GUID_SERENUM_BUS_ENUMERATOR は古い形式の識別子、[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)プラグ アンド プレイ (PnP) のシリアル ポート。 Microsoft Windows 2000 以降を使用して、 [ **GUID_DEVINTERFACE_SERENUM_BUS_ENUMERATOR** ](guid-devinterface-serenum-bus-enumerator.md)このクラスの新しいインスタンスのクラス識別子。

<a name="remarks"></a>注釈
-------

WDK には、シリアル列挙子のサンプルが用意されています ([*serenum*](https://msdn.microsoft.com/library/windows/hardware/ff546505))。 シリアルの列挙子では、GUID_SERENUM_BUS_ENUMERATOR を使用して、このデバイスのインターフェイス クラスのインスタンスを登録します。 含まれている serenum サンプル、 *src\\カーネル*WDK のディレクトリ。

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

 

 






