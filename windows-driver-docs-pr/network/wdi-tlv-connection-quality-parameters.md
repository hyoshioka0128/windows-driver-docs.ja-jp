---
title: WDI_TLV_CONNECTION_QUALITY_PARAMETERS
description: WDI_TLV_CONNECTION_QUALITY_PARAMETERS では、目的の Wi-fi 接続品質のヒントを含む TLV です。
ms.assetid: A371FD3A-5BF9-4921-AB8E-1651789FA9A1
ms.date: 07/18/2017
keywords:
- WDI_TLV_CONNECTION_QUALITY_PARAMETERS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 3ce8680e00d04276a7bb7fd80a96db8ae9ae977c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357259"
---
# <a name="wditlvconnectionqualityparameters"></a>WDI\_TLV\_接続\_品質\_パラメーター


WDI\_TLV\_接続\_品質\_パラメーターが必要な Wi-fi 接続品質のヒントを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xA3

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値


| 型   | 説明                                                                                                                          |
|--------|--------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | 必要な Wi-fi 接続品質ヒントで定義された[ **WDI\_接続\_品質\_ヒント**](https://msdn.microsoft.com/library/windows/hardware/dn897807)します。 |

 

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

 

 




