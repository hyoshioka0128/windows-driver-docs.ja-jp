---
title: IP データを処理するための制御ノード
description: IP データを処理するための制御ノード
ms.assetid: 6195ffe9-d20c-4687-8d45-abbfc17ba2fa
keywords:
- WDK BDA のノードを制御します。
- WDK BDA ノード
- IP データ処理 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74dbc450a7c83e74839cc5b35a50b66b18b246b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374198"
---
# <a name="control-nodes-for-processing-ip-data"></a>IP データを処理するための制御ノード





次のシーケンスと図は、受信のデジタル信号の一部である IP データのデータ フローを説明します。

1.  受信デバイスは、IP のデータを受信し、トランスポート ストリームの一部として PC バス経由で IP データを渡します。

2.  デマルチプレクサーはトランスポート ストリームを受信し、IP データを含むプライベート セクションを渡します。

3.  プライベート セクションは、マルチ プロトコルのカプセル化を削除し、IP データを出力する、マルチ プロトコルのカプセル化 (MPE) パーサーによって受信されます。 MPE パーサーでは、IPSink フィルターに IP データを渡します。

4.  IPSink フィルターは、ブロードキャスト NDISIP ミニポート ドライバーに、プライベート インターフェイスを介して IP データを渡します。

5.  NDISIP ミニポート ドライバーは、仮想の NDIS ミニポートとしてインストールされます。 NDISIP ミニポート ドライバーでは、NDIS を IP データを送信します。

6.  NDIS は、その他の NDIS アダプターの場合と同様に、TCP/IP と Windows ソケット (WinSock) によって IP データを伝達します。

**注**  以降 Windows Vista では、IPSink フィルターはサポートされていません。

 

![ip データ フローを示す図](images/ipdata.png)

 

 




