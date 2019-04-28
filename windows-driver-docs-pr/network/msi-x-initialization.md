---
title: MSI-X の初期化
description: MSI-X の初期化
ms.assetid: 64e79ea1-eb6b-4c94-8bad-dd892b712b28
keywords:
- ネットワーク、初期化中に MSI X WDK
- メッセージ シグナル割り込み WDK ネットワーク、初期化しています
- Msi WDK ネットワーク、初期化しています
- MSI X の初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e2a26a6f0fc848fc6a5e8cf82271d0eaba7af62
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382640"
---
# <a name="msi-x-initialization"></a>MSI-X の初期化





MSI X のサポートには、MSI の初期化には、リソース要件をフィルター処理する関数を確立するミニポート ドライバーを事前登録フェーズが必要です。 この関数は MSI X メッセージごとに割り込みアフィニティを変更したり、ドライバーは行ベースでの割り込みを登録している場合は、メッセージの割り込みリソースを削除、 [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。

NDIS 呼び出される前に事前登録フェーズが発生した、 [ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。 行ベースの割り込みのミニポート ドライバーも登録ミニポート アダプターの初期化中に MSI 割り込み*MiniportInitializeEx*します。

このセクションの内容:

[MSI X の事前登録](msi-x-pre-registration.md)

[MSI X リソース フィルター](msi-x-resource-filtering.md)

[登録して、MSI の割り込みの登録を解除](registering-and-deregistering-an-msi-interrupt.md)

 

 





