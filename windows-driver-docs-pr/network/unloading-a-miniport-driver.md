---
title: ミニポート ドライバーをアンロード
description: ミニポート ドライバーをアンロード
ms.assetid: c5199a0f-31c3-42e4-8758-cbe480dff682
keywords:
- ミニポート ドライバー WDK ネットワーク、アンロード
- NDIS ミニポート ドライバー WDK、アンロード
- アンロードのミニポート ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bf7a723cacca92bd84c6a0b7b464ea3c9ef09ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554014"
---
# <a name="unloading-a-miniport-driver"></a>ミニポート ドライバーをアンロード





NDIS ミニポート ドライバーに関連付けられているドライバー オブジェクトを指定します、 [**アンロード**](https://msdn.microsoft.com/library/windows/hardware/ff564886)ルーチン。 システム コール、*アンロード*ルーチンときに、すべてのデバイス ドライバー サービスが削除されていること。 NDIS の提供、*アンロード*ミニポート ドライバーの日常的な。 NDIS ミニポート ドライバーを呼び出す[ *MiniportDriverUnload* ](https://msdn.microsoft.com/library/windows/hardware/ff559378)関数を*アンロード*ルーチン。

ミニポート ドライバーを呼び出す必要があります[ **NdisMDeregisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563578)から*MiniportDriverUnload*します。

ミニポート ドライバーの*MiniportDriverUnload*関数は、個々 のドライバーのリソースを解放もする必要があります。 システムの後にドライバー アンロード操作が完了*MiniportDriverUnload*を返します。

機能、 *MiniportDriverUnload*関数は、ドライバー固有です。 一般的な規則として*MiniportDriverUnload*ドライバーの初期化中に実行された操作を元に戻す必要があります。 ドライバーの初期化の詳細については、[ミニポート ドライバーの初期化](initializing-a-miniport-driver.md)を参照してください。

 

 





