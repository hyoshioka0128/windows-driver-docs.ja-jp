---
title: ミニポート アダプターのコンテキスト
description: ミニポート アダプターのコンテキスト
ms.assetid: cb43d02d-cf52-46a4-b56d-aa3afcbd0ca5
keywords:
- 論理アダプター WDK ネットワーク
- コンテキスト WDK ミニポートアダプター
- ミニポートアダプター WDK ネットワーク、コンテキスト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 704f2e08434f274f53f609f4f44fbbbe40f700bb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844259"
---
# <a name="miniport-adapter-context"></a>ミニポート アダプターのコンテキスト





NDIS は、*ミニポートアダプター*と呼ばれるソフトウェアオブジェクトを使用して、システム内の各仮想ネットワークデバイスまたは物理ネットワークデバイスを表します。 このオブジェクトは NDIS によって管理され、ミニポートドライバーとプロトコルドライバーには非透過です。 NDIS は、この構造体へのハンドルをミニポートドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数に渡します。 その後、ミニポートドライバーは、このハンドルが指定するミニポートアダプターに関連する**Ndis * Xxx*** 関数のすべての呼び出しにこのハンドルを提供します。

ミニポートドライバーを呼び出して、それが管理するミニポートアダプターを初期化すると、ミニポートアダプターを表す独自の内部データ構造が作成されます。 ドライバーは、ミニポート*アダプターコンテキスト*と呼ばれるこの構造を使用して、ドライバーがミニポートアダプターを管理するために必要なデバイス固有の状態情報を保持します。 ドライバーは、この構造体へのハンドルを NDIS に渡します。 ミニポートアダプターコンテキストの指定の詳細については、「[アダプターの初期化](initializing-a-miniport-adapter.md)」を参照してください。

ミニポートアダプターに関連するミニポートドライバーの*Miniportxxx*関数のいずれかを ndis が呼び出すと、ndis はミニポートアダプターコンテキストを渡して、ドライバーに対する正しいミニポートアダプターを識別します。 ミニポートアダプターのコンテキストは、ミニポートドライバーによって所有および管理され、NDIS およびプロトコルドライバーに対して非透過的です。

 

 





