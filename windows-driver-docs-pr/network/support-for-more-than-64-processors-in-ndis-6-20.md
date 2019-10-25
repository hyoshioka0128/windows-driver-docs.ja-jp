---
title: NDIS 6.20 の 64 を超えるプロセッサのサポート
description: NDIS 6.20 の 64 を超えるプロセッサのサポート
ms.assetid: 3fb2a09c-e2dd-48b8-a631-3793bd023ef0
keywords:
- NDIS 6.20 WDK、64を超えるプロセッサのサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2712415bf1f98b72c97dd3489f05a6ee6280338
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841802"
---
# <a name="support-for-more-than-64-processors-in-ndis-620"></a>NDIS 6.20 の 64 を超えるプロセッサのサポート





NDIS 6.20 インターフェイスでは、64を超えるプロセッサのサポートが導入されています。 以前のバージョンの NDIS は、64プロセッサ (x86 バージョンのオペレーティングシステムでは 32) 以下に制限されています。

以前の実装との下位互換性を維持するために、NDIS はプロセッサグループをサポートしています。 64を超えるプロセッサをサポートするように更新されていないソフトウェアは、既定でプロセッサグループゼロに設定できます。

64を超えるプロセッサをサポートするために、NDIS 6.20 以降では、これらのインターフェイスの更新バージョンが提供されます。

-   [Receive Side Scaling (RSS)](ndis-receive-side-scaling2.md)

-   プロセッサ情報デバイスドライバーインターフェイス (「 [NDIS システム情報機能](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)」を参照)

-   リソース割り当て (「 [NDIS メモリ管理インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)」を参照)

-   読み取りおよび書き込みロック (「 [NDIS Read Write Lock Reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)」を参照)

Ndis デバイスドライバーのインターフェイス要素の一部は、NDIS 6.20 以降のドライバーでは廃止されています。 互換性のために残されているインターフェイスの詳細については、「 [NDIS 6.20 の古いインターフェイス](obsolete-interfaces-in-ndis-6-20.md)」を参照してください。

 

 





