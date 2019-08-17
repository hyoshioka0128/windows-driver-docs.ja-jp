---
title: NDIS MSI-X の概要
description: NDIS MSI-X の概要
ms.assetid: 5bb374c8-9354-42d3-9754-42e8ff42bdb9
keywords:
- ミニポートドライバー WDK ネットワーク、MSI-X
- NDIS ミニポートドライバー WDK、MSI-X
- MSI-X WDK ネットワーク
- メッセージシグナル割り込み (WDK ネットワーク)
- Msi WDK ネットワーク
- WDK ネットワークを中断する
- 割り込みアフィニティ WDK ネットワーク
- WDK ネットワークを中断します
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea37bf478cac493a78e5a0fbd1a38b1a9d92c5ef
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565650"
---
# <a name="overview-of-ndis-msi-x"></a>NDIS MSI-X の概要





メッセージシグナル割り込み (Msi) は、ネットワークデバイスとそのミニポートドライバーが使用できる従来の行ベースの割り込みに代わる手段を提供します。 Windows Vista 以降のオペレーティングシステムでは、次の2種類の Msi がサポートされています。PCI v1.0 MSI および PCI v1.0 MSI-X。

MSI をサポートするミニポートドライバーでは、*割り込みアフィニティ*を指定できます。これは、ドライバーのメッセージ割り込みサービスルーチンが実行される中央処理ユニット (cpu) のサブセットです。 各 MSI-X メッセージに対して割り込みの関係を指定できます。たとえば、デバイスの "近接" に関して、Non-uniform Memory Access (NUMA) アーキテクチャを使用しているコンピューターで、割り込みのアフィニティを指定できます。

MSI-X サポートは、特に receive side scaling (RSS) をサポートするネットワークインターフェイスカード (Nic) に対して、大きなパフォーマンス上の利点を提供できます。 Receive side scaling の詳細については、「 [Receive Side scaling](ndis-receive-side-scaling2.md)」を参照してください。

行ベースの割り込みの詳細については、「[割り込みの管理](managing-interrupts.md)」を参照してください。

このセクションの内容:

[MSI-X の初期化](msi-x-initialization.md)

[MSI 割り込みの処理](handling-an-msi-interrupt.md)

[MSI 割り込みとの同期](synchronizing-with-an-msi-interrupt.md)

[MSI-X テーブルエントリの CPU 関係の変更](changing-the-cpu-affinity-of-msi-x-table-entries.md)

 

 





