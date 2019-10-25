---
title: RF データ交換シーケンスにタグを付ける
description: 次の図は、T1T、T2T、T3T、ISO-DEP などのさまざまなリーダーライタープロトコルの StateRfDiscovered と StateRfDataXchg の状態シーケンスを示しています。
ms.assetid: F5911609-4531-44B3-9629-CD0A27D40324
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afc480e6142acd70cf6e14926869b38135c36ad5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827359"
---
# <a name="tag-rf-data-exchange-sequence"></a>RF データ交換シーケンスにタグを付ける


次の図は、T1T、T2T、T3T、ISO-DEP などのさまざまなリーダーライタープロトコルの StateRfDiscovered および StateRfDataXchg の状態シーケンスを示しています。 RF インターフェイスのアクティブ化の後に検出された StateRfDiscovered への移行が発生します。 StateRfDiscovery に複数のリモートエンドポイントまたは複数のプロトコルがある場合、NFC CX は単一のエンドポイントとプロトコルを選択します。 NFC の優先-DEP を使用した DEP は、コントローラーでは、寄託オプションがサポートされていない場合の相互運用性を向上させるために、NFC CX に実装されています。 StateRfDiscovered は、StateRfDataXchg に移行する前に、NFC CX が初期のプレゼンスチェックを実行する移行状態です。 Reader/writer モードの場合、StateRfDataXchg は NDEF 操作の次のシーケンスに分類されます。 check NDEF、read または write NDEF、およびプレゼンスチェックです。 また、ドライバーは、アプリケーション層からの要求に応じて、書式設定、読み取り専用、低レベルのタグ操作などの追加操作をこの状態で実行します。 NFC CX は、ISO DEP を除き、すべての NCI 標準プロトコル (および ISO15693) に対してフレーム RF インターフェイスをサポートしていることに注意してください。 Iso dep プロトコルをサポートするには、NFC コントローラーで ISO DEP RF インターフェイスがサポートされている必要があります。

![t1t rf データ交換シーケンス](images/rfdataexchangesequence.png)

T2T RF データ交換シーケンスの例を次に示します。

![t2t rf データ交換シーケンス](images/t2trfdataexchangesequence.png)

T3T RF データ交換シーケンスの例を次に示します。

![t3t rf データ交換シーケンス](images/t3trfdataexchangesequence.png)

ISO DEP の RF データ交換シーケンスを次に示します。

![iso-dep rf データ交換シーケンス](images/iso-dep-rfdataexchangesequence.png)

リモート RF エンドポイントと交換するデータがない場合、NFC CX は StateRfDataXchg でのプレゼンスチェックを実行します。 これは、リモート RF エンドポイントが DH から範囲外に移動したかどうかを判断するために使用されます。 シーケンス図に示されているように、さまざまなタグの種類のプレゼンスチェックには次のコマンドが使用されます。

-   NFC フォーラムタイプ1タグの場合、NFC CX は、UID を返す読み取り識別 (RID) コマンドを使用して、プレゼンスチェックの検出を実行します。

-   NFC フォーラムタイプ2タグの場合、NFC CX は、16バイトのブロックデータを返す READ block コマンドを使用して、プレゼンスチェックの検出を実行します。

-   NFC フォーラムタイプ3タグの場合、NFC CX は RF\_T3T\_ポーリング\_CMD NCI command (SENSF) を使用して、プレゼンスチェックの検出を実行します。

-   NFC フォーラムタイプ4のタグの場合、NFC CX は空の I ブロック交換を使用して、プレゼンスチェックの検出を実行します。

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC クラス拡張 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
