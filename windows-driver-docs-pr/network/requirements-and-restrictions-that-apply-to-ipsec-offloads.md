---
title: 要件と IPsec オフロードに適用される制限
description: 要件と IPsec オフロードに適用される制限
ms.assetid: c016d6dd-f760-4340-8d56-9bd69e4fe84e
keywords:
- WDK の IPsec ESP により保護されたパケットのオフロード、要件
- AH で保護されたパケット WDK IPsec オフロード、要件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d739bf72342434c1b6e8e2cd97273f191d5b97e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560633"
---
# <a name="requirements-and-restrictions-that-apply-to-ipsec-offloads"></a>要件と IPsec オフロードに適用される制限

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]




次の要件と制限事項は、(IPsec) オフロード インターネット プロトコル セキュリティに適用されます。

-   NIC には、セキュリティ アソシエーション (SA) のテーブルを維持する必要があります。 これは、キーを含める必要がなくなるため、パフォーマンスが向上または AH と ESP での処理に必要なその他の情報は、パケットを送信します。

-   NIC を 1 つのパケットのペイロードを AH と ESP の両方を処理することがあります。 ここでは、NIC では、AH と ESP の整合性 (認証) アルゴリズムの次の組み合わせをサポートする必要があります。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">AH</th>
    <th align="left">ESP</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>MD5</p></td>
    <td align="left"><p>MD5</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>SHA 1</p></td>
    <td align="left"><p>SHA 1</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>MD5</p></td>
    <td align="left"><p>SHA 1</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>SHA 1</p></td>
    <td align="left"><p>MD5</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>MD5</p></td>
    <td align="left"><p>Null (場合にのみ、NIC は、null 暗号化をサポートする)</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>SHA 1</p></td>
    <td align="left"><p>Null (場合にのみ、NIC は、null 暗号化をサポートする)</p></td>
    </tr>
    </tbody>
    </table>

     

<!-- -->

-   DES アルゴリズムをサポートしている NIC には、これらのアルゴリズムを必要とする初期化ベクター (IV) を生成する必要があります。

-   NIC を実行する IPsec タスクのみの AH の暗号化チェックサムまたはチェックサムの ESP (またはその両方) を処理し、暗号化と ESP ペイロードの暗号化を解除していること。 送信パケットの場合は、TCP/IP トランスポートは埋め込み、すべてのヘッダーを作成します、番号を再生し、送信先アドレスと IPsec プロトコルの組み合わせに固有の SPI 値を選択します。 パケットの受信、TCP/IP トランスポートは受信ポリシー チェックを実行、ハンドルはリプレイの検出と防止、および監査イベントのハンドル。

-   送信パケットの場合は、TCP/IP トランスポートはできません (暗号化されたデータの開始を示す) などの明示的なオフセット オフロード ドライバーは、この情報を使用して特定のセキュリティ アソシエーション (SA) から簡単に判断できますので、プロセス、パケットです。

-   IPsec プロトコルを使用したパケットの認証ヘッダー (AH) またはカプセル化セキュリティ ペイロード (ESP) のヘッダー (またはその両方) での認証情報が必要です。 IPsec パケットの認証がないことはできません。

-   IPsec タスクは、IP 断片化を必要とするパケットの送信またはオフロードされず IP 断片化から再構築を必要とするパケットを受信します。

-   IPsec タスクでは、送信はオフロードされずと、負荷分散のミニポート ドライバーに渡されるパケットを受信します。 負荷分散の詳細については、次を参照してください。[負荷分散とフェールオーバー](https://msdn.microsoft.com/library/windows/hardware/ff549197)します。

 

 





