---
title: 印刷のモニターの作成
description: 印刷のモニターの作成
ms.assetid: ca5600fc-9e2c-4735-90c4-9509c31dee29
keywords:
- 印刷スプーラーは印刷モニター、WDK をカスタマイズします。
- スプーラが印刷、印刷のモニターを WDK のカスタマイズ
- 印刷スプーラー コンポーネント WDK、印刷のモニターをカスタマイズします。
- 印刷モニター WDK
- 印刷のモニターの作成
- モニターの WDK を印刷します。
- 印刷モニター WDK、印刷のモニタについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f14a998e82249d1b8e79819531f88b13f9a42ba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529454"
---
# <a name="writing-a-print-monitor"></a>印刷のモニターの作成





印刷のモニターは、適切なポート ドライバーに印刷スプーラー サービスからの印刷データ ストリームの指導を担当します。 2 つの種類の印刷モニターが定義されている--[言語モニター](language-monitors.md)と[ポート モニター](port-monitors.md)します。 このセクションでは、両方のモニターの種類を説明し、設計と実装のガイドラインを提供します。

次のトピックが用意されています。

[言語モニター](language-monitors.md)

[ポート モニター](port-monitors.md)

[言語およびポート モニターの相互作用](language-and-port-monitor-interaction.md)

[印刷のモニターが定義されている関数](functions-defined-by-print-monitors.md)

[印刷のモニターの初期化](initializing-a-print-monitor.md)

[ポートを開いたり、閉じたりします。](opening-and-closing-a-port.md)

[印刷ジョブの印刷](printing-a-print-job.md)

[ポートの管理](managing-a-port.md)

[TCPMON Xcv インターフェイス](tcpmon-xcv-interface.md)

[WSDMON ポート モニター](wsdmon-port-monitor.md)

[クラスター化されたプリント サーバーで使用するための印刷のモニターに変換します。](converting-print-monitors-for-use-with-clustered-print-servers.md)

[印刷のモニターをインストールします。](installing-a-print-monitor.md)

 

 




