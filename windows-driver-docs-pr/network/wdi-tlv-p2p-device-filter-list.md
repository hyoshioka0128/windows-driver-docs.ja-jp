---
title: WDI_TLV_P2P_DEVICE_FILTER_LIST
description: WDI_TLV_P2P_DEVICE_FILTER_LIST は、Wi-Fi Direct デバイスの検出中に検索するには、Wi-Fi Direct デバイスの一覧を含む TLV とグループの所有者です。
ms.assetid: 56D1E6BD-41E3-4869-A821-334012B781A7
ms.date: 07/18/2017
keywords:
- WDI_TLV_P2P_DEVICE_FILTER_LIST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 9124439f9d88e64a2d5a2f19cc6a42209c99f814
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366566"
---
# <a name="wditlvp2pdevicefilterlist"></a>WDI\_TLV\_P2P\_デバイス\_フィルター\_一覧


WDI\_TLV\_P2P\_デバイス\_フィルター\_一覧は、Wi-Fi Direct デバイスの検出中に検索するには、Wi-Fi Direct デバイスの一覧を含む TLV とグループの所有者。

## <a name="tlv-type"></a>TLV 型


0xCE

## <a name="length"></a>長さ


配列のサイズをバイト単位で[ **WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071)構造体。 配列には、1 つ以上の構造を格納する必要があります。

## <a name="values"></a>値


| 型                                                  | 説明                                                                                         |
|-------------------------------------------------------|-----------------------------------------------------------------------------------------------------|
| [**WDI\_MAC\_アドレス**](https://msdn.microsoft.com/library/windows/hardware/dn926071)\[\] | Wi-Fi Direct デバイスと Wi-Fi Direct デバイスの検出中に検索するグループの所有者の一覧。 |

 

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

 

 




