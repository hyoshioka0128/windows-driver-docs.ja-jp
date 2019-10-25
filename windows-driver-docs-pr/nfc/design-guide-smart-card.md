---
title: スマート カード設計ガイド
description: スマート カード設計ガイド
ms.assetid: 721A1530-B7B4-4373-9006-356A0A601349
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f3389aab004b28e499febf2114ad65942ead5b0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843427"
---
# <a name="smart-card-design-guide"></a>スマート カード設計ガイド


スマートカード DDI を使用すると、NFC デバイスドライバーへの呼び出し元が、NFC contactless スマートカードで低レベルのスマートカード操作を実行できます。 これには、カードの到着/出発通知をリッスンしたり、ATR、UID、履歴バイト情報などのスマートカードのメタデータを読み取ったり、APDUs を使用して特定の NFC カードで読み取り/書き込み操作を実行したりすることが含まれます。 ISO14443 に準拠していないカード (ストレージカードとも呼ばれます) については、「4.3.7」セクションで、ストレージカードでサポートされる低レベルのプリミティブコマンドへの APDUs の変換について説明しています。 Ioctl はスマートカードデバイスドライバーインターフェイスを構成し、すべての\_アクセスとメソッド\_バッファリングされた\_ファイルを使用します。 次のスマートカード DDI は、Windows \[1\] によって指定されたスマートカードドライバーの Ioctl の最小サブセットであり、NFC contactless スマートカードへのアクセスをサポートしています。

``` syntax
GUID_DEVINTERFACE_SMARTCARD_READER
“{50DD5230-BA8A-11D1-BF5D-0000F805F530}”
```

## <a name="unsupported-ioctls"></a>サポートされていない Ioctl


次の Ioctl は、contactless スマートカード操作には適用されないため、NFC スマートカード操作ではサポートされません。そのため、ドライバーはサポートされていないエラーコードを返す可能性があります。

-   スマートカード\_の IOCTL\_取り出し
-   \_最後の\_エラーを取得するための IOCTL\_スマートカード\_
-   スマートカード\_の IOCTL\_飲み込む

## <a name="smart-card-attributes"></a>スマートカードの属性
Windows スマートカード DDI には、Get 属性と Set 属性に対する IOCTL 要求が含まれています。 NFC contactless reader をサポートするための最小要件を満たすために、最小限のリーダーと ICC 状態の GET_ATTRIBUTE のみをサポートしています。 詳細については、「[サポートされているスマートカードの属性](smart-card-attributes.md)」を参照してください。

## <a name="in-this-section"></a>このセクションの内容


-   [機能フロー](functional-flow.md)
-   [シーケンスの例](example-sequence.md)
-   [メモリカードの要件](storage-card-requirements.md)
-   [サポートされるスマートカードの属性](smart-card-attributes.md)
-   [PC/SC インターフェイス](pc-sc-interface.md)
 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[スマートカード DDI とコマンドリファレンス](https://docs.microsoft.com/previous-versions/dn905601(v=vs.85))  

