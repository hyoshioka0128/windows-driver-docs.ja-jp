---
title: WDI_TLV_SCAN_MODE
description: WDI_TLV_SCAN_MODE では、スキャン モード パラメーターを含む TLV です。
ms.assetid: 9F954B66-4F1D-48F2-9316-BE623DF0CAE6
ms.date: 07/18/2017
keywords:
- WDI_TLV_SCAN_MODE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 2d98b7e76e96207dc44c5c888721c86f5a555654
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330522"
---
# <a name="wditlvscanmode"></a>WDI\_TLV\_スキャン\_モード


WDI\_TLV\_スキャン\_モードは、スキャン モード パラメーターを含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x6

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                                | 説明                                                                                                                                                                                                                       |
|-----------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                               | フル スキャンの手順を繰り返す回数。 この値が 0 に設定されている場合は、ホストにより、タスクが中止されるまでスキャンを繰り返す必要があります。                                                                     |
| [**WDI\_スキャン\_型**](https://msdn.microsoft.com/library/windows/hardware/dn926115)       | 実行されるスキャンの種類を指定します。 場合 WDI\_スキャン\_型\_アクティブに設定されている、デバイスはアクティブ チャネルのみをスキャンする必要があります。                                                                                                |
| UINT8                                               | ライブ更新が必要なかどうかと、上記の推奨される調整のロジックで見つかったときに、検出されたエントリを報告する必要がありますを指定します。 この値は、Microsoft コンポーネントが BSS リストのキャッシュを管理する場合に常に true です。 |
| [**WDI\_スキャン\_トリガー**](https://msdn.microsoft.com/library/windows/hardware/dn926114) | スキャンのトリガーを指定します。                                                                                                                                                                                               |

 

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

 

 




