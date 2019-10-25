---
title: MSI-X の初期化
description: MSI-X の初期化
ms.assetid: 64e79ea1-eb6b-4c94-8bad-dd892b712b28
keywords:
- MSI-X WDK ネットワーク, 初期化
- メッセージシグナルによる WDK ネットワークの割り込み、初期化
- Msi WDK ネットワーク, 初期化
- 初期化 (MSI-X を)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c4081f69b5c312127bc85a1ce87ad41bfb70606
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844216"
---
# <a name="msi-x-initialization"></a>MSI-X の初期化





Msi-X をサポートするには、MSI の初期化に事前登録フェーズが必要です。このフェーズでは、リソース要件をフィルター処理する関数がミニポートドライバーによって確立されます。 この関数は、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数の行ベースの割り込みにドライバーが登録する場合、各 MSI-X メッセージの割り込み関係を変更するか、メッセージの割り込みリソースを削除することができます。

プリ登録フェーズは、NDIS が[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出す前に発生します。 行ベースの割り込みと同様に、ミニポートドライバーは*MiniportInitializeEx*のミニポートアダプターの初期化中に MSI 割り込みも登録します。

このセクションの内容:

[MSI-X 事前登録](msi-x-pre-registration.md)

[MSI-X リソースフィルター処理](msi-x-resource-filtering.md)

[MSI 割り込みの登録と登録解除](registering-and-deregistering-an-msi-interrupt.md)

 

 





