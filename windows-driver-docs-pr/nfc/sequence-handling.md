---
title: シーケンス処理
description: NFC CX によって公開されている特定のドライバーのシーケンスを登録することで NCI の非標準の拡張機能のサポートについて説明します。
ms.assetid: D0BE9827-2A15-4AA5-ADB9-80071ED37583
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 970c46b7769b7c742430fdead9b686169684071f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386503"
---
# <a name="sequence-handling"></a>シーケンス処理


最も非標準の NCI 機能と拡張機能のさまざまなベンダーから NFCC ファームウェアによって実装されるチップセットの設定、ファームウェアのダウンロード、およびハードウェアのチューニングに関連しています。 これらの非標準の拡張機能は、NFC CX によって公開されている特定のドライバーのシーケンスを登録することによって、NFC クライアント ドライバーによってサポートできます。 クライアント ドライバーはを通じて特定のシーケンスのハンドラーの登録、 [ **NfcCxRegisterSequenceHandler** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxregistersequencehandler)関数。 通常初期化中に行われ、後に呼び出す必要がある[ **NfcCxDeviceInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxdeviceinitialize)します。 これらのハンドラーが呼び出すことで登録解除[ **NfcCxUnRegisterSequenceHandler** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxunregistersequencehandler)デバイスのシャット ダウン中にします。 クライアント ドライバーのシーケンスのハンドラーのコールバックが呼び出された後、NFC CX ドライバーは発行されません NCI コマンド NFC クライアント ドライバーがその処理が完了するまで。 NFC CX の完了を通知する前に、コント ローラーを任意の数の I/O 要求を発行するクライアントにより、非同期にするのには、これらのシーケンス ハンドラー コールバックが設計されています。 NFC CX では、ウォッチドッグのタイマー機構を使用して、ハングした状態を調べます。 ウォッチドッグ タイマーは、クライアントがシーケンスのハンドラーの完了前に期限が切れると、バグ チェックがトリガーされ、UMDF フレームワークによって UMDF ホスト プロセスが終了します。

シーケンスのハンドラーの一部として追加のロジックを実装する NFC クライアント ドライバーの要件を次に示します。

-   これらのシーケンスを処理するときに、NFC クライアントから送信された任意の NCI コマンドでは、NFC CX で指定された現在の状態の整合性に違反しないことを確認してください。 そのため、NFC のデバイスの適切に機能していることを確認するには、この要件の NFC クライアントを処理する必要があります。 たとえば、完全なシーケンスの初期化を処理するときに、クライアント ドライバー発行する NCI CORE\_リセット\_チップセットをリセットするには、「cmd」。
-   NFC クライアント ドライバーは、NCI 応答と、コント ローラーに送信する NCI コマンドによって生成される通知が NFC CX に送信しないことを確認する必要がある[ **NfcCxNciReadNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxncireadnotification)関数。 それ以外の場合、NFC CX NCI のステート マシンが、NFCC と交換コマンドを使用して同期が取得するために必要です。

## <a name="in-this-section"></a>このセクションの内容


-   [シーケンス](sequences.md)
-   [シーケンスのフラグ](sequence-flags.md)
-   [初期化シーケンス](initialization-sequence.md)
-   [NFCEE 探索シーケンス](nfcee-discovery-sequence.md)
-   [RF 探索シーケンス](rf-discovery-sequence.md)
-   [RF タグ データの交換シーケンス](tag-rf-data-exchange-sequence.md)
-   [P2P RF データの交換シーケンス](p2p-rf-data-exchange-sequence.md)
-   [カードのエミュレーション RF シーケンス](card-emulation-rf-sequence.md)

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[NFC クラスの拡張機能 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
