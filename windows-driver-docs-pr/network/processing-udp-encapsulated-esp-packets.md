---
title: ESP の UDP カプセル化パケットを処理します。
description: ESP の UDP カプセル化パケットを処理します。
ms.assetid: b5b10a2c-1080-4c21-a187-1c0aff30b229
keywords:
- WDK の IPsec ESP パケットを UDP カプセル化オフロード、処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5801bcc4d86b78b162b55e51740eba605c073bc0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532205"
---
# <a name="processing-udp-encapsulated-esp-packets"></a>ESP の UDP カプセル化パケットを処理します。

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]




NIC は、ポート 4500 の UDP カプセル化パケットを受信するときに、パケットが IKE (コントロール) のパケットをまたはにパケットを ESP (データ) がかどうかを確認します。 IKE と ESP パケットの UDP カプセル化の種類の説明は、次を参照してください。 [UDP ESP カプセル化型](udp-esp-encapsulation-types.md)します。

-   パケットが、IKE パケットの場合は、NIC は、パケットをさらに IPsec に関連する処理を行わなくても、ミニポート ドライバーに渡します。

-   パケットが、ESP パケットの場合は、NIC がパケットの受信 SA (または SAs トランスポート経由のトンネル パケットの場合) が NIC にオフロードされる現在あるかどうかを確認します
    -   受信の SAs は、NIC に現在はオフロードされず、NIC はさらに IPsec に関連する処理を行わなくても、ミニポート ドライバーにパケットを渡します。
    -   受信の SAs は、NIC にオフロード現在、NIC は、SAs に関連付けられているパーサー エントリで指定されたカプセル化の種類を使用して、パケットを解析します。 NIC は、パケットに ESP ペイロードをし処理」の説明に従って[受信パスでの IPsec タスク オフロード](offloading-ipsec-tasks-in-the-receive-path.md)します。

着信 ESP パケットの UDP カプセル化されたトランスポート経由のトンネル パケット」の説明に従って場合[UDP ESP カプセル化型](udp-esp-encapsulation-types.md)NIC には、ESP ペイロードではないと、パケットのトンネル モードの部分の最初に復号化しますUDP カプセル化されます。 次の NIC は、パケットの UDP カプセル化のトンネル モードの部分を処理します。

 

 





