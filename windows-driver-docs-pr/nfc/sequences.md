---
title: シーケンス
description: このトピックでは、NFC CX ドライバーのシーケンスを説明します。
ms.assetid: 92FDF18F-B42B-43F2-914A-CA7E986EE0DF
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b04abeeb6db5ae7bf7b31d1fd2743c744bb09f82
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386505"
---
# <a name="sequences"></a>シーケンス


このトピックでは、NFC CX ドライバーのシーケンスを説明します。

| Sequence                    | 説明                                                                                                                                                                                                                                                                                                                                                                                               |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SequencePreInit             | CX によって初期化状態を遷移するまでのアイドル時に呼び出されます (つまり、NFC CX で初期化の開始前に)。 CORE を含む NCI コマンドが存在しない\_リセット\_CMD が NFC CX で NFC コント ローラーに送信されました。 このシーケンスで、クライアントは、任意の非 NCI コマンドを呼び出すことができます。 NCI のコマンドは、どちら CORE 以降、コント ローラーに送信しないでください\_リセット\_CMD もコア\_INIT\_CMD は、コント ローラーに送信されました。 |
| SequenceInitComplete        | NFC CX NCI のリセット、NCI 初期化 NFC コント ローラーの構成などの初期化の完了後すぐには、CX によって呼び出されます。                                                                                                                                                                                                                                          |
| SequencePreRfDiscStart      | RF を通じてつまり RF 探索を開始する前に CX によって呼び出される\_DISCOVER\_cmd. クライアント ドライバーでは、この機会を使用して、検出ループに最適化を含む関連 RF 構成をすべて実行します。                                                                                                                                                                                        |
| SequenceRfDiscStartComplete | RF 検出の開始後すぐには、CX によって呼び出されます。 任意の構成後の検出の開始は、この機能拡張ポイントをサポートできます。                                                                                                                                                                                                                                                      |
| SequencePreRfDiscStop       | RF 検出のループを停止する前に、CX によって呼び出されます。                                                                                                                                                                                                                                                                                                                                                    |
| SequenceRfDiscStopComplete  | 探索のループが停止した直後に呼び出されます。 クライアント ドライバーでは、スタンバイ モードのすべての構成を有効にするのにこの機能拡張ポイントを使用できます。                                                                                                                                                                                                                                                         |
| SequencePreNfceeDisc        | NFCEE 探索を開始する前に CX によって呼び出されます。 NFCEE 検出は、非アクティブ化された探索ループでは発生します。 クライアント ドライバーは、このシーケンスを使用して、電力の最適化の後の初期化を無効にされているでした内部 NFC NFCEE インターフェイスを有効にすることができます。                                                                                                                         |
| SequenceNfceeDiscComplete   | Post NFCEE 検出操作をすぐに呼び出されます。                                                                                                                                                                                                                                                                                                                                                       |
| SequencePreShutdown         | シャット ダウンの開始前に呼び出されます。                                                                                                                                                                                                                                                                                                                                                                       |
| SequenceShutdownComplete    | シャット ダウン シーケンスが完了した後に、CX によって呼び出されます。 クライアント ドライバーとクリーンアップ、NCI 状態を維持できます。                                                                                                                                                                                                                                                                                               |
| SequencePreRecovery         | 致命的なエラーのための復元シーケンスを実行する必要がある場合に、CX によって呼び出されます。 クライアント ドライバーは、このシーケンスを使用して、診断用のメモリ ダンプをキャプチャできます。                                                                                                                                                                                                                                    |
| SequenceRecoveryComplete    | 復元シーケンスを使用して、ドライバーが作業状態に戻すには、完了した後、CX によって呼び出されます                                                                                                                                                                                                                                                                                             |

 

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[NFC クラスの拡張機能 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  

