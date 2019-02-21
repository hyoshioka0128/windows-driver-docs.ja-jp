---
title: 一般的な I/O ターゲット
description: 一般的な I/O ターゲット
ms.assetid: e5527aa2-a63f-49d8-aa9a-f91efd2ae9ad
keywords:
- 一般的な I/O WDK KMDF をターゲットします。
- I/O ターゲット WDK KMDF、[全般]
- ローカルの I/O WDK KMDF をターゲットします。
- リモートの I/O WDK KMDF をターゲットします。
- 一般的な I/O に関する一般的な I/O ターゲット WDK KMDF をターゲットと
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05e5f456965913d030ee3c86b3eb272c856e9c67
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527494"
---
# <a name="general-io-targets"></a>一般的な I/O ターゲット





一般的な I/O ターゲットは、USB 要求のブロックなどの特殊なデバイスに固有のデータ形式をサポートしていません。 ドライバーは、一般的な I/O ターゲットにデータを送信、I/O ターゲットを解釈できる形式で書き込みバッファー データに格納する必要があります。 同様に、ドライバーは、一般的な I/O ターゲットからのデータを読み取り、ドライバーできる必要があります、ターゲットから受け取ったデータ バッファーの内容を解釈します。

一般的な I/O ターゲットは、ローカルまたはリモートのいずれかには。

<a href="" id="local-i-o-targets"></a>ローカルの I/O ターゲット  
各関数の framework ベースのドライバー、フィルター ドライバー、およびミニポート ドライバーは、各ドライバーのデバイスのローカル I/O ターゲットがあります。 デバイスのローカルの I/O の対象は、常に、ドライバー スタックで次の下位ドライバーです。

<a href="" id="remote-i-o-targets"></a>リモートの I/O ターゲット  
リモートの I/O ターゲットは、別のドライバー スタックまたは (ほとんど)、現在のドライバーのスタック内の別のドライバーの先頭を表します。

このセクションの内容:

-   [一般的な I/O のターゲットの初期化](initializing-a-general-i-o-target.md)

-   [一般的な I/O ターゲットへの I/O 要求を送信します。](sending-i-o-requests-to-general-i-o-targets.md)

-   [一般的な I/O ターゲットの状態を制御します。](controlling-a-general-i-o-target-s-state.md)

-   [一般的な I/O のターゲットに関する情報を取得します。](obtaining-information-about-a-general-i-o-target.md)

 

 





