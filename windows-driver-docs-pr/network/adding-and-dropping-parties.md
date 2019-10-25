---
title: パーティーの追加と削除
description: パーティーの追加と削除
ms.assetid: ec4c10a4-6a8f-4c1c-858e-954b98922e84
keywords:
- 接続指向の NDIS WDK、パーティ
- CoNDIS WDK ネットワーク、パーティ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 050bb032934eaee21e720868ddc616a4349d7d1b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838241"
---
# <a name="adding-and-dropping-parties"></a>パーティーの追加と削除





接続指向クライアントは、 [**NdisClMakeCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclmakecall)で開始された送信マルチポイント呼び出しにパーティを追加できます。 また、接続指向クライアントは、独自の判断で、または削除するリモートパーティの要求で、multipoint 呼び出しからパーティを削除することもできます。

このセクションの内容:

[Multipoint 呼び出しへのパーティの追加](adding-a-party-to-a-multipoint-call.md)

[Multipoint 呼び出しからのパーティの削除](dropping-a-party-from-a-multipoint-call.md)

[Multipoint 呼び出しからパーティを削除するための受信要求](incoming-request-to-drop-a-party-from-a-multipoint-call.md)

 

 





