---
title: Wi-Fi Direct 印刷
description: Windows 8.1 と Windows の以降のバージョンは、Wi-Fi Direct (WFD) 経由で印刷をサポートします。
ms.assetid: B2FC1293-F9E4-43A4-84BF-21EF8C3D27E0
ms.date: 01/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 22ef2a07b95369716d567bb4bfd4c8d3cb94ca63
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557913"
---
# <a name="wi-fi-direct-printing"></a>Wi-Fi Direct 印刷


Windows 8.1 と Windows の以降のバージョンは、Wi-Fi Direct (WFD) 経由で印刷をサポートします。

Windows Wi-Fi Direct 印刷サポートを実装する印刷デバイスは、次で実装する必要があります。

-   Wi-Fi Direct 垂直ペアリング
-   すべての論理デバイスを物理デバイスでのコンテナーの ID に一致します。
-   WSD/Ws-print

このトピックとサブトピックで使用される定義。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>用語</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WFD</p></td>
<td><p>Wi-Fi Direct</p></td>
</tr>
<tr class="even">
<td><p>DAF</p></td>
<td><p>デバイスの関連付けのフレームワーク</p></td>
</tr>
<tr class="odd">
<td><p>DAS</p></td>
<td><p>デバイス関連付けサービス</p></td>
</tr>
<tr class="even">
<td><p>GO</p></td>
<td><p>グループの所有者</p></td>
</tr>
<tr class="odd">
<td><p>PBC</p></td>
<td><p>クリック 1 回の接続</p></td>
</tr>
</tbody>
</table>

 

Wi-Fi Direct 印刷サポートに関する一般的な情報が記載されて、 [Wi-Fi Direct 印刷の概要](wfd-overview.md)します。 参照してください[Wi-Fi Direct 印刷実装](wfd-implementation.md)Wi-Fi Direct 印刷を実装する方法の詳細について。

## <a name="certification-requirements"></a>認定の要件


新しい認定の要件は、この機能に関連付けではありません。 参照してください**関連ドキュメント**、下の該当する既存の要件。

## <a name="hck-requirements"></a>HCK の要件


実装されている場合のデバイスが Wi-Fi Direct の Wi-fi Alliance 証明する必要があります。

使用可能なすべてのトランスポート経由の適用の HCK テストを実行するための要件を含む印刷デバイスのすべての既存認定要件が適用されます。 パートナーは、変更があった場合に、Windows 認定チームによって発行された公式の認定要件ドキュメントを常に参照してください。

**注**  Wi-Fi Direct の The Wi-fi Alliance の認定要件です。 Wi-fi Alliance Wi-Fi Direct サービスは個別の仕様と、この時点で、Windows でサポートされていません。

 

## <a name="related-documents"></a>関連ドキュメント


関連情報については、次のトピックを参照してください。

[コンテナー Id の概要](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-container-ids)
[PnP-x:プラグ アンド プレイ Extensions for Windows 仕様](https://msdn.microsoft.com/windows/hardware/gg463082)
[Wi-fi Alliance - Wi-Fi Direct 業界に関するホワイト ペーパー](https://go.microsoft.com/fwlink/p/?LinkId=784967)
 

 




