---
title: シーケンス
description: このトピックでは、NFC CX ドライバーシーケンスについて説明します。
ms.assetid: 92FDF18F-B42B-43F2-914A-CA7E986EE0DF
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e2271b23018f157c61b68e2bfb9665c64981d3f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826176"
---
# <a name="sequences"></a>シーケンス


このトピックでは、NFC CX ドライバーシーケンスについて説明します。

| Sequence                    | 説明                                                                                                                                                                                                                                                                                                                                                                                               |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SequencePreInit             | アイドル状態遷移中 (つまり、NFC CX による初期化が開始される前) に、CX によって呼び出されます。 NFC CX によって送信された、コア\_リセット\_CMD を含む NCI コマンドが NFC コントローラーに送信されていません。 このシーケンスでは、クライアントは NCI 以外の任意のコマンドを呼び出すことができます。 NCI コマンドをコントローラーに送信することはできません。これは、CORE\_RESET\_CMD と CORE\_INIT\_CMD がコントローラーに送信されていないためです。 |
| SequenceInitComplete        | NCI reset、NCI の初期化、NFC コントローラーの構成など、NFC CX の初期化が完了した直後に、CX によって呼び出されます。                                                                                                                                                                                                                                          |
| SequencePreRfDiscStart      | Rf の検出を開始する前に CX によって呼び出され、RF\_\_CMD を検出します。 クライアントドライバーは、この機会を利用して、検出ループの最適化など、関連する RF 構成を実行できます。                                                                                                                                                                                        |
| SequenceRfDiscStartComplete | RF 検出の開始直後に、CX によって呼び出されます。 この機能拡張ポイントを使用すると、すべての構成の探索後の開始をサポートできます。                                                                                                                                                                                                                                                      |
| SequencePreRfDiscStop       | RF 検出ループを停止する前に、CX によって呼び出されます。                                                                                                                                                                                                                                                                                                                                                    |
| SequenceRfDiscStopComplete  | 検出ループが停止した直後に呼び出されます。 クライアントドライバーは、この機能拡張ポイントを使用して、任意のスタンバイモード構成を有効にすることができます。                                                                                                                                                                                                                                                         |
| SequencePreNfceeDisc        | NFCEE 検出を開始する前に、CX によって呼び出されます。 検出ループが非アクティブになると、NFCEE 検出が発生します。 クライアントドライバーは、このシーケンスを使用して、電力の最適化の初期化後に無効になっている可能性がある内部 NFC NFCEE インターフェイスを有効にすることができます。                                                                                                                         |
| SequenceNfceeDiscComplete   | NFCEE の検出操作が直ちに呼び出されました。                                                                                                                                                                                                                                                                                                                                                       |
| SequencePreShutdown         | シャットダウンの開始前に呼び出されました。                                                                                                                                                                                                                                                                                                                                                                       |
| SequenceShutdownComplete    | シャットダウンシーケンスの完了後に、CX によって呼び出されました。 クライアントドライバーは、保持されているすべての NCI 状態をクリーンアップできます。                                                                                                                                                                                                                                                                                               |
| SequencePreRecovery         | 重大なエラーによって回復シーケンスを実行する必要がある場合に、CX によって呼び出されます。 クライアントドライバーは、このシーケンスを使用して、診断のために RAM ダンプをキャプチャできます。                                                                                                                                                                                                                                    |
| SequenceRecoveryComplete    | 回復シーケンスの完了後、およびドライバーが作業状態に戻るときに、CX によって起動されます。                                                                                                                                                                                                                                                                                             |

 

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC クラス拡張 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

