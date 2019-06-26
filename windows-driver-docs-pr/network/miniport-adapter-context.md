---
title: ミニポート アダプターのコンテキスト
description: ミニポート アダプターのコンテキスト
ms.assetid: cb43d02d-cf52-46a4-b56d-aa3afcbd0ca5
keywords:
- 論理アダプター WDK ネットワーク
- WDK ミニポート アダプタのコンテキスト
- ミニポート アダプタの WDK ネットワーク、コンテキスト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b57eba4ae33598eeba55abcdba0821fd82dceee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373976"
---
# <a name="miniport-adapter-context"></a>ミニポート アダプターのコンテキスト





NDIS と呼ばれるソフトウェア オブジェクトを使用して、*ミニポート アダプター*をシステム内の各仮想または物理ネットワーク デバイスを表します。 このオブジェクトは、NDIS が管理し、ミニポート ドライバーとプロトコル ドライバーにに対して非透過的です。 NDIS ミニポート ドライバーのこの構造体へのハンドルを渡します[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数。 ミニポート ドライバーが、その後にすべての呼び出しでは、このハンドルを提供**Ndis * Xxx*** ハンドルを指定するミニポート アダプターに関連する関数。

ミニポート ドライバーは、管理しているミニポート アダプターを初期化するために呼び出されると、ミニポート アダプターを表す独自の内部データ構造を作成します。 ドライバーと呼ばれるこの構造体を使用して、*ミニポート アダプター コンテキスト*ミニポート アダプターを管理するドライバーに必要なデバイス固有の状態情報を維持するためにします。 ドライバーは、NDIS この構造体へのハンドルを渡します。 ミニポート アダプタのコンテキストを指定する方法については、次を参照してください。 [、アダプターの初期化](initializing-a-miniport-adapter.md)します。

NDIS を呼び出すのミニポート ドライバーのいずれかと*MiniportXxx* NDIS ミニポート アダプターに関連する関数が正しいミニポート アダプターは、ドライバーを識別するために、ミニポート アダプターのコンテキストを渡します。 ミニポート アダプタのコンテキストが所有し、ミニポート ドライバーによって保持されるが NDIS してプロトコル ドライバーに不透明であるとします。

 

 





