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
ms.openlocfilehash: 84cc8b7a14a1df6ddc3e45a9e8eb6457e03d6e28
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353294"
---
# <a name="error-handling"></a>エラー処理


このトピックでは、エラー処理の NFC クライアントの要件について説明します。

-   NFC のクライアント ドライバーは、コント ローラーへの書き込み要求を実行するときにエラーが発生した場合は、NFC CX を通知する責任を負います。 エラー状態を受信すると、NFC CX は、回復、再試行を実行するか、エラー状態を入力します。

-   シーケンスの呼び出しを完了したときに、NFC のクライアント ドライバーはエラーを報告できます。 現在の状態によっては、NFC CX は回復または enter エラー状態に入力します。

-   NFCC、検出、クラッシュすると、コアを送信することが予想\_リセット\_NTF をホストします。 コアを受信すると、NFC CX\_リセット\_NTF は適切な回復を実行します。

-   回復不可能なエラーが検出されると、クライアントは、NFC/CX HostActionRestart を通じてドライバーの完全な再起動を行うまたは HostActionUnload を使用してドライバーをアンロードする要求に通知できます。

-   NFC のクライアント ドライバーで WDF verifier Api を使用して、NFC クライアント ドライバー (参照の予約済みの範囲のバグ チェックのコードを使用してクラッシュをトリガーすることが予想が NFC クライアント (たとえば、メモリ破損の検出など) のユーザー モード クラッシュをトリガーする場合は、NfcCxBugCodes.h の詳細)。 既定ではプロセスの共有が有効になっているためには、NFC のクライアント ドライバーは、どうしても必要なときにそれ以外の場合、停止を引き起こす可能性 WUDF ドライバーのホスト プロセスでは、その他のドライバーだけにこのメカニズムを使用して重要です。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[NFC クラスの拡張機能 (CX) リファレンス](https://msdn.microsoft.com/library/windows/hardware/dn905536)  

