---
title: WDI_TLV_P2P_INSTANCE_NAME_HASH
description: WDI_TLV_P2P_INSTANCE_NAME_HASH はハッシュを含む TLV「インスタンス名、サービスの種類」のです。
ms.assetid: A29D0339-93A8-43EB-8C22-DD7A7DC2147C
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_INSTANCE_NAME_HASH ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 3e504755b4048efaa2c728c09f11ba684de4a505
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347269"
---
# <a name="wditlvp2pinstancenamehash"></a>WDI\_TLV\_P2P\_インスタンス\_名前\_ハッシュ


WDI\_TLV\_P2P\_インスタンス\_名前\_ハッシュのハッシュを含む TLV は、「インスタンス名、サービスの種類」のです。

**注**  この TLV は、Windows 10 バージョン 1607、WDI バージョン 1.0.21 で追加されました。

 

## <a name="tlv-type"></a>TLV 型


0x12C

## <a name="length"></a>長さ


サイズ (バイト単位) で、 [ **WDI\_P2P\_サービス\_名前\_ハッシュ**](https://msdn.microsoft.com/library/windows/hardware/dn926103)構造体。

## <a name="values"></a>値


| 型                                                                    | 説明                                |
|-------------------------------------------------------------------------|--------------------------------------------|
| [**WDI\_P2P\_サービス\_名前\_ハッシュ**](https://msdn.microsoft.com/library/windows/hardware/dn926103) | 「インスタンス名、サービスの種類」のハッシュです。 |

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




