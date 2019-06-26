---
title: Hyper-V 拡張可能スイッチ転送コンテキスト
description: Hyper-V 拡張可能スイッチ転送コンテキスト
ms.assetid: B2BF07B5-FA44-4994-9605-EFF4A0B9179F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0797e6616485fa1a436d388c522466ab386cbc9b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382231"
---
# <a name="hyper-v-extensible-switch-forwarding-context"></a>Hyper-V 拡張可能スイッチ転送コンテキスト


[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造に、HYPER-V 拡張可能スイッチのデータ パスを通過する各パケットには、アウト オブ バンド (OOB) データが含まれています。 このデータは、パケットが発信された場所、およびパケット配信のための 1 つまたは複数の宛先ポートからの発信元ポートを指定します。 この OOB データと呼ばれる、*転送コンテキスト拡張可能スイッチ*します。

このセクションには、コンテキストを転送する拡張可能スイッチに関する以下のトピックが含まれています。

[HYPER-V 拡張可能スイッチのコンテキストのデータ型の転送](hyper-v-extensible-switch-forwarding-context-data-types.md)

[コンテキストを転送する HYPER-V 拡張可能スイッチの管理](managing-the-hyper-v-extensible-switch-forwarding-context.md)

 

 





