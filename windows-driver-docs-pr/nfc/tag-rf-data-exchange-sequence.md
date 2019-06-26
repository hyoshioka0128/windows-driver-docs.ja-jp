---
title: RF データ交換シーケンスにタグを付ける
description: 次の図では、StateRfDiscovered と StateRfDataXchg 状態のシーケンスを示して T1T、T2T、T3T、および ISO DEP. などのさまざまなリーダー/ライター プロトコル
ms.assetid: F5911609-4531-44B3-9629-CD0A27D40324
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 007d50b7d062583e226f8d5bdba38ab925c716d9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353285"
---
# <a name="tag-rf-data-exchange-sequence"></a>RF データ交換シーケンスにタグを付ける


次の図では、StateRfDiscovered と StateRfDataXchg 状態シーケンスを示して T1T、T2T、T3T、および ISO DEP. などのさまざまなリーダー/ライター プロトコル StateRfDiscovered への移行は、RF インターフェイスのアクティブ化の後に発生します。 複数のリモート エンドポイントまたは StateRfDiscovery で複数のプロトコルでは、場合は、NFC CX は、1 つのエンドポイントとプロトコルを選択します。 NFC-DEP ISO DEP 経由での優先順位は、bail オプションは、コント ローラーでサポートされていない場合に、相互運用性の NFC CX に実装されます。 StateRfDiscovered が NFC CX は StateRfDataXchg に移行する前に、初期の存在チェックを実行します。 移行の状態です。 読み取り/書き込みモードで StateRfDataXchg 分かれて NDEF 操作の次のシーケンス: NDEF の確認、読み取りまたは書き込み NDEF、プレゼンスの確認後にします。 ドライバーには、書式設定、アプリケーション レイヤーからの要求によってこの状態で読み取り専用の低レベルのタグの操作のような追加の操作も実行します。 NFC CX がすべて NCI の標準プロトコル (として ISO15693) ISO DEP. を除きフレーム RF インターフェイスをサポートすることに注意してください。 ISO DEP プロトコルをサポートするために、NFC コント ローラーでは、ISO DEP RF インターフェイスをサポートする必要があります。

![t1t rf データの交換シーケンス](images/rfdataexchangesequence.png)

T2T RF のデータの交換シーケンスを次に示します。

![t2t rf データの交換シーケンス](images/t2trfdataexchangesequence.png)

T3T RF のデータの交換シーケンスを次に示します。

![t3t rf データの交換シーケンス](images/t3trfdataexchangesequence.png)

ISO DEP RF データの交換シーケンスを次に示します。

![iso dep rf データ シーケンスを交換します。](images/iso-dep-rfdataexchangesequence.png)

NFC CX リモート RF エンドポイントと交換するデータがない場合に、StateRfDataXchg でプレゼンス チェックを実行します。 これは、リモート RF エンドポイントが範囲外移動かどうか、DH から決定に使用されます。 ように、シーケンス図では、次のコマンドは、さまざまなタグの種類のプレゼンスの確認に使用されます。

-   NFC フォーラム タイプ 1 のタグの NFC CX はプレゼンス チェックの検出を実行するのに UID を返す、読み取りの Id (RID) コマンドを使用します。

-   NFC フォーラム種類 2 のタグの NFC CX はプレゼンス チェックの検出を実行するのに、16 バイトのブロックでデータを返す、読み取りブロックのコマンドを使用します。

-   RF を使用している NFC CX の NFC フォーラム種類 3 のタグの\_T3T\_ポーリング\_プレゼンス チェックの検出を実行する CMD NCI コマンド (SENSF)。

-   NFC フォーラム型 4 のタグの NFC CX はプレゼンス チェックの検出を実行するのに、空はブロック exchange を使用します。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[NFC クラスの拡張機能 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
