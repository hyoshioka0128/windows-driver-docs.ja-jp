---
title: エラー処理
description: このトピックでは、NFC クライアントのエラー処理の要件について説明します。
ms.assetid: 52376A1F-9ADD-4297-ADF9-A1EBF5714316
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed9bc4bacba5a1a850f7a75b96207f479d0561e3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843416"
---
# <a name="error-handling"></a>エラー処理


このトピックでは、NFC クライアントのエラー処理の要件について説明します。

-   NFC クライアントドライバーは、コントローラーへの書き込み要求を実行するときにエラーが発生した場合に、NFC CX に通知を行います。 エラー状態を受信したときに、NFC CX は再試行、回復、またはエラー状態の入力のいずれかを実行します。

-   NFC クライアントドライバーは、シーケンス呼び出しの完了時にエラーを報告できます。 現在の状態に応じて、NFC CX は回復またはエラー状態の入力を入力します。

-   NFCC でクラッシュが発生した場合は、NTF のコア\_リセット\_をホストに送信することが期待されます。 コア\_リセット\_NTF を受信したときに、NFC CX は適切な回復を実行します。

-   クライアントは、回復不能なエラーを検出したときに、NFC CX に対して HostActionRestart による完全なドライバーの再起動を実行するように通知したり、Hostactionrestart を使用してドライバーをアンロードするように要求したりすることができます。

-   NFC クライアントがユーザーモードのクラッシュをトリガーする必要がある場合 (たとえば、メモリの破損を検出する場合) は、nfc クライアントドライバーが WDF verifier Api を使用して、NFC クライアントドライバーの予約済みの範囲でバグチェックコードを使用してクラッシュをトリガーすることが想定されます (「」を参照)。詳細については、「Nfccxバグコード」を参照してください。 プロセス共有は既定で有効になっているため、NFC クライアントドライバーは、必要な場合にのみこのメカニズムを使用することが重要です。そうしないと、WUDF ドライバーホストプロセスで他のドライバーが停止する可能性があります。

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC クラス拡張 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

