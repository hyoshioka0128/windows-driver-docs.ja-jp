---
title: WDI_TLV_MULTICAST_CIPHER_ALGO_LIST
description: WDI_TLV_MULTICAST_CIPHER_ALGO_LIST では、マルチキャストの暗号アルゴリズムの一覧を含む TLV です。
ms.assetid: 55CDD295-6BDA-4F3A-B01F-FC9D5FB38355
ms.date: 07/18/2017
keywords:
- WDI_TLV_MULTICAST_CIPHER_ALGO_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: cb8c56995e7c8f6dc1a5a49174a18fbe734fd613
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385263"
---
# <a name="wditlvmulticastcipheralgolist"></a>WDI\_TLV\_マルチキャスト\_暗号\_ALGO\_一覧


WDI\_TLV\_マルチキャスト\_暗号\_ALGO\_リストは、マルチキャストの暗号アルゴリズムの一覧を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x3D

## <a name="length"></a>長さ


配列のサイズをバイト単位で[ **WDI\_暗号\_アルゴリズム**](https://msdn.microsoft.com/library/windows/hardware/dn897802)構造体。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型                                                            | 説明                              |
|-----------------------------------------------------------------|------------------------------------------|
| [**WDI\_暗号\_アルゴリズム**](https://msdn.microsoft.com/library/windows/hardware/dn897802)\[\] | マルチキャストの暗号アルゴリズムの配列。 |

 

<a name="requirements"></a>必要条件
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

 

 




