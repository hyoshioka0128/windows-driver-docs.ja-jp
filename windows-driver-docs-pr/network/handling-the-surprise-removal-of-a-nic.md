---
title: NIC の突然の取り外しの処理
description: NIC の突然の取り外しの処理
ms.assetid: afd94749-8f2a-4cce-a646-1f616a845a0e
keywords:
- 突然削除 WDK ネットワーク
- Nic WDK ネットワー キング、突然の削除
- ネットワーク インターフェイス カード WDK ネットワー キング、突然の削除
- プラグ アンド プレイ WDK NDIS ミニポート、突然 NIC の削除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3132b3b85b026a8ef707a9cdf07653a608f3cb5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573619"
---
# <a name="handling-the-surprise-removal-of-a-nic"></a>NIC の突然の取り外しの処理





突然削除では、ユーザーが実行中のシステムから、システム ユーザー インターフェイス (UI) を通じて事前通知することがなく、ネットワーク インターフェイス カード (NIC) を削除するときに発生します。

Windows Vista およびそれ以降のバージョンのオペレーティング システムのミニポート ドライバーでは、突然の削除を処理できる必要があります。 具体的には、NDIS ミニポート ドライバーを Windows Driver Model (WDM) の下端は、このようなイベントを処理できる必要があります。 NDIS WDM のミニポート ドライバーが突然削除を処理しない場合、保留中のミニポート ドライバーが突然削除前に、基になるバス ドライバーに送信される Irp を完了できません。

Windows Vista およびそれ以降のバージョンでは、ハードウェアを直接制御しません (WDM 下端のミニポート ドライバー) などのミニポート ドライバーが、NDIS を設定する必要があります\_ミニポート\_属性\_突然\_削除\_を呼び出すときに、[ok] の属性フラグ[ **NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672)します。 このフラグを設定すると、警告が、ユーザーは、NIC の突然の削除を実行するときに表示されないできません。 驚きの削除を処理できないミニポート ドライバーでは、このフラグは設定しないでください。

サポートでは削除が突然--のコンテキスト外での通常操作中に突然削除の検出を試みる必要がある自体のミニポート ドライバー [ *MiniportDevicePnPEventNotify*](https://msdn.microsoft.com/library/windows/hardware/ff559369)します。 NIC が削除されると、通常、NIC の I/O ポートを読み取ろうとして結果戻り値を 1 に設定するすべてのビットを持つ値になります。 ミニポート ドライバーでは、このような値を読み取り場合、もう少し明確なテストでのハードウェアの存在をチェックする必要があります。 たとえば、ミニポート ドライバーは、I/O ポートに値を書き込むし、そのポートから、値を読み取るから再試行してください。 ミニポート ドライバーは、NIC の I/O レジスタで有効な値のチェックもでした。 このような方法で突然の削除を検出、ミニポート ドライバーは割り込み DPC で削除された NIC のレジスタの読み取りを試行するときは、無限ループ内でハングできなくなります. この方法で応答を停止したミニポート ドライバーがドライバーの呼び出し元から NDIS を停止する*MiniportDevicePnPEventNotify*関数。

 

 





