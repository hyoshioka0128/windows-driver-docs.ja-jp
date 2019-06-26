---
title: ミニポート ドライバーのアンロード
description: ミニポート ドライバーのアンロード
ms.assetid: c5199a0f-31c3-42e4-8758-cbe480dff682
keywords:
- ミニポート ドライバー WDK ネットワーク、アンロード
- NDIS ミニポート ドライバー WDK、アンロード
- アンロードのミニポート ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cf5d0bccf3bc2a06c749da8fd66852dddbc3841
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382093"
---
# <a name="unloading-a-miniport-driver"></a>ミニポート ドライバーのアンロード





NDIS ミニポート ドライバーに関連付けられているドライバー オブジェクトを指定します、 [**アンロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)ルーチン。 システム コール、*アンロード*ルーチンときに、すべてのデバイス ドライバー サービスが削除されていること。 NDIS の提供、*アンロード*ミニポート ドライバーの日常的な。 NDIS ミニポート ドライバーを呼び出す[ *MiniportDriverUnload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_unload)関数を*アンロード*ルーチン。

ミニポート ドライバーを呼び出す必要があります[ **NdisMDeregisterMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismderegisterminiportdriver)から*MiniportDriverUnload*します。

ミニポート ドライバーの*MiniportDriverUnload*関数は、個々 のドライバーのリソースを解放もする必要があります。 システムの後にドライバー アンロード操作が完了*MiniportDriverUnload*を返します。

機能、 *MiniportDriverUnload*関数は、ドライバー固有です。 一般的な規則として*MiniportDriverUnload*ドライバーの初期化中に実行された操作を元に戻す必要があります。 ドライバーの初期化の詳細については、次を参照してください。[ミニポート ドライバーの初期化](initializing-a-miniport-driver.md)します。

 

 





