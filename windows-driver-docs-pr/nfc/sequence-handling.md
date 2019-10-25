---
title: シーケンス処理
description: NFC CX によって公開されている特定のドライバーシーケンスを登録することによる、非標準の NCI 拡張機能のサポートについて説明します。
ms.assetid: D0BE9827-2A15-4AA5-ADB9-80071ED37583
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a615b56a746b8f508e655aadb9e0f60a9b35979
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834533"
---
# <a name="sequence-handling"></a>シーケンス処理


異なるベンダーの NFCC ファームウェアによって実装されている標準以外の NCI 機能と拡張機能のほとんどは、チップセットの構成、ファームウェアのダウンロード、およびハードウェアのチューニングに関連しています。 このような非標準の拡張機能は、nfc CX によって公開されている特定のドライバーシーケンスに登録することによって、NFC クライアントドライバーでサポートできます。 クライアントドライバーは、 [**Nfccxregistersequencehandler**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxregistersequencehandler)関数を介して特定のシーケンスハンドラーを登録します。 通常は初期化中に実行され、 [**Nfccxdeviceinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxdeviceinitialize)の後に呼び出す必要があります。 これらのハンドラーは、デバイスのシャットダウン中に[**Nfccxunregistersequencehandler**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxunregistersequencehandler)を呼び出すことによって登録解除されます。 クライアントドライバーのシーケンスハンドラーコールバックが呼び出されると、nfc CX ドライバーは、NFC クライアントドライバーの処理を完了するまで、NCI コマンドを発行しません。 これらのシーケンスハンドラーのコールバックは非同期になるように設計されているため、クライアントは任意の数の i/o 要求をコントローラーに発行できます。これにより、クライアントは、NFC の完了を通知する前に任意の数の i/o 要求を発行できます。 NFC CX は、ウォッチドッグタイマー機構を使用して、ハング状態を判断します。 クライアントによるシーケンスハンドラーの完了前にウォッチドッグタイマーが期限切れになると、バグチェックがトリガーされ、umdf ホストプロセスは UMDF フレームワークによって終了されます。

次に、シーケンスハンドラーの一部として追加のロジックを実装するときの NFC クライアントドライバーの要件を示します。

-   これらのシーケンスを処理するときに NFC クライアントによって送信された NCI コマンドは、NFC CX によって指定された現在の状態の整合性に違反しないようにする必要があります。 そのため、nfc クライアントはこの要件に対処して、NFC デバイスが正しく機能するようにする必要があります。 例として、初期化の完了シーケンスを処理する場合、クライアントドライバーは NCI CORE\_リセット\_CMD を発行してチップセットをリセットする必要があります。
-   NFC クライアントドライバーは、コントローラーに送信する NCI コマンドによって生成される NCI の応答と通知が、NFC CX の[**Nfccxncireadnotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxncireadnotification)関数に送信されないようにする必要があります。 そうしないと、NFC CX NCI ステートマシンが NFCC と交換するコマンドと同期しなくなるため、この操作が必要になります。

## <a name="in-this-section"></a>このセクションの内容


-   [文字列](sequences.md)
-   [シーケンスフラグ](sequence-flags.md)
-   [初期化シーケンス](initialization-sequence.md)
-   [NFCEE 検出シーケンス](nfcee-discovery-sequence.md)
-   [RF 検出シーケンス](rf-discovery-sequence.md)
-   [RF データ交換シーケンスにタグを付ける](tag-rf-data-exchange-sequence.md)
-   [P2P RF データ交換シーケンス](p2p-rf-data-exchange-sequence.md)
-   [カードエミュレーション RF シーケンス](card-emulation-rf-sequence.md)

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC クラス拡張 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
