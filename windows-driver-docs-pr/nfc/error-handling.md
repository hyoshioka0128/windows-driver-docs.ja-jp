---
title: エラー処理
description: このトピックでは、エラー処理の NFC クライアントの要件について説明します。
ms.assetid: 52376A1F-9ADD-4297-ADF9-A1EBF5714316
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 893154fc4afe84e60a0b9a98e2795dc433c1b85e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370525"
---
# <a name="error-handling"></a>エラー処理


このトピックでは、エラー処理の NFC クライアントの要件について説明します。

-   NFC のクライアント ドライバーは、コント ローラーへの書き込み要求を実行するときにエラーが発生した場合は、NFC CX を通知する責任を負います。 エラー状態を受信すると、NFC CX は、回復、再試行を実行するか、エラー状態を入力します。

-   シーケンスの呼び出しを完了したときに、NFC のクライアント ドライバーはエラーを報告できます。 現在の状態によっては、NFC CX は回復または enter エラー状態に入力します。

-   NFCC、検出、クラッシュすると、コアを送信することが予想\_リセット\_NTF をホストします。 コアを受信すると、NFC CX\_リセット\_NTF は適切な回復を実行します。

-   回復不可能なエラーが検出されると、クライアントは、NFC/CX HostActionRestart を通じてドライバーの完全な再起動を行うまたは HostActionUnload を使用してドライバーをアンロードする要求に通知できます。

-   NFC のクライアント ドライバーで WDF verifier Api を使用して、NFC クライアント ドライバー (参照の予約済みの範囲のバグ チェックのコードを使用してクラッシュをトリガーすることが予想が NFC クライアント (たとえば、メモリ破損の検出など) のユーザー モード クラッシュをトリガーする場合は、NfcCxBugCodes.h の詳細)。 既定ではプロセスの共有が有効になっているためには、NFC のクライアント ドライバーは、どうしても必要なときにそれ以外の場合、停止を引き起こす可能性 WUDF ドライバーのホスト プロセスでは、その他のドライバーだけにこのメカニズムを使用して重要です。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[NFC クラスの拡張機能 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  

