---
title: 初期化シーケンス
description: 次の図は、高度な一連の初期化中に、NFC CX および、NFCC によって交換される NCI パケットを示しています。
ms.assetid: 4977E1D4-2546-4573-B555-FA87DB8A2168
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a18d7283f36b8dc9fae66fc59a3ec1c5c7351a3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375121"
---
# <a name="initialization-sequence"></a>初期化シーケンス


次の図は、高度な一連の初期化中に、NFC CX および、NFCC によって交換される NCI パケットを示しています。 、初期化の開始前に、NFC CX ドライバーは、登録されている場合に、クライアント ドライバーの初期化前のシーケンスのハンドラーを呼び出します。 StateInit には、次の大まかなシーケンスが構成されています。NCI の初期化、パラメーター、および RF インターフェイスおよび RF プロトコル マッピングの標準の NCI 構成、NCI をリセットします。 ただし、NFC のクライアント ドライバーなどの NFC CX のインターフェイスの関数を使用して初期化中に使用される NCI 構成パラメーターのいくつかの既定値を設定できます[ **NfcCxSetRfDiscoveryConfig** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxsetrfdiscoveryconfig)と[**NfcCxSetLlcpConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxsetllcpconfig)します。 初期化が完了した後、初期化のシーケンスの完了ハンドラーが呼び出されます。 初期化が完了した後は、次の状態は、StateRfIdle です。

![初期化シーケンス](images/initializationsequence.png)

NFC のクライアント ドライバーからファームウェアのダウンロード操作の処理、NFCC の適切な機能の主な要件の 1 つです。 NFC CX デザインは、コント ローラーにファームウェアをダウンロードするための複数の異なるデザインをサポートするために十分な柔軟性があります。

いくつかチップセットでは、ファームウェアのバージョン管理については、ファームウェアのダウンロードが必要なかどうかを判断する NCI の初期化が必要です。 このようなデザインでは、次に示すよう、ファームウェアのダウンロードを実行するための NFC CX および NFC クライアント ドライバーのステート マシンが表示されます。 青の状態が NFC CX で指定された状態に対応し、灰色の状態は、NFC のクライアント ドライバーの状態に対応します。 Post の初期化シーケンスの完了ハンドラー、クライアント ドライバーでつまり NCI の初期化はコアから現在のバージョンを確認します。\_INIT\_RSP メッセージ、およびファームウェアのダウンロード操作が必要な場合を判断します。 'No' の場合は、次の状態に NFC CX ドライバーの通常の状態遷移が続行します。 場合 'Yes'、クライアント ドライバーは、再起動を実行する NFC CX を要求します。 シャット ダウンの完了時に、NFC クライアント ドライバーは、ファームウェアのダウンロードを実装できます。

![ファームウェアのダウンロード後の初期化](images/initializationsequence1.png)

一部 NFCC ファームウェアの実装では、帯域外機構、つまり、ファームウェアのダウンロードが必要なかどうかを判断する、NCI のコンテキスト外があります。 このような場合、前の初期化シーケンスを処理するときに、NFC のクライアント ドライバーは、ファームウェアのダウンロードが必要なかどうかを判断するには、そのコネクタ状態を実装できます。 'Yes' の場合、ファームウェアのダウンロード操作によって実行されてクライアント ドライバー。 ファームウェアのダウンロードは必要ありません。 [いいえ]、[次へ] の状態の通常の操作が続行します。 次の図は、ステート マシンのファームウェアのダウンロード前-NCI の初期化処理を示します。

![ファームウェアのダウンロード前の初期化](images/firmwaredownloadpreinitialization.png)

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[NFC クラスの拡張機能 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  

