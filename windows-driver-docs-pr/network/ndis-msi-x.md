---
title: NDIS MSI-X
description: NDIS MSI-X
ms.assetid: 5bb374c8-9354-42d3-9754-42e8ff42bdb9
keywords:
- ミニポート ドライバー WDK ネットワー キング、MSI X
- NDIS ミニポート ドライバー WDK、MSI X
- MSI X WDK ネットワーク
- メッセージ シグナル割り込み WDK ネットワーク
- Msi WDK ネットワーク
- WDK のネットワークを中断します。
- 割り込みアフィニティ WDK ネットワーク
- net WDK の割り込み
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8228dcc831573067e11d94bd0c7da2caf54f766a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573280"
---
# <a name="ndis-msi-x"></a>NDIS MSI-X





メッセージ シグナル割り込み (Msi) は、ネットワーク デバイスとそのミニポート ドライバーが使用できる従来の行ベースの割り込みの代替を提供します。 Windows Vista 以降のオペレーティング システムには、Msi の 2 種類がサポートされています。PCI V2.2 MSI and PCI V3.0 MSI-X.

MSI をサポートするミニポート ドライバーを指定できます、*割り込みアフィニティ*ドライバーのメッセージの割り込みサービス ルーチンは、上で実行される中央処理装置 (Cpu) のサブセットであります。 MSI X メッセージごとに--割り込みアフィニティを指定するなどを指定できます、Non-uniform Memory Access (NUMA) アーキテクチャについて特定の Cpu に自分のデバイスの「近接」でコンピューターとのアフィニティを中断します。

MSI X のサポートは、特にのネットワーク インターフェイス カード (Nic) のサポートが側 scaling (RSS) を受信する場合の大幅なパフォーマンスの利点を提供できます。 詳細については、受信側のスケーリングを参照してください[Receive Side Scaling](ndis-receive-side-scaling2.md)します。

詳細については、行ベースの割り込みは、[管理の割り込み](managing-interrupts.md)を参照してください。

このセクションの内容:

[MSI X の初期化](msi-x-initialization.md)

[MSI 割り込みを処理します。](handling-an-msi-interrupt.md)

[MSI 割り込みとの同期](synchronizing-with-an-msi-interrupt.md)

[MSI X テーブル エントリの CPU 関係を変更します。](changing-the-cpu-affinity-of-msi-x-table-entries.md)

 

 





