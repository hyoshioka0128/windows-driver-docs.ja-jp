---
title: Hyper-v 拡張可能スイッチ転送コンテキストの概要
description: Hyper-v 拡張可能スイッチ転送コンテキストの概要
ms.assetid: B2BF07B5-FA44-4994-9605-EFF4A0B9179F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb734efaf5db91ba8f32f94767bb5e2a547b0d1b
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565676"
---
# <a name="hyper-v-extensible-switch-forwarding-context-overview"></a>Hyper-v 拡張可能スイッチ転送コンテキストの概要


Hyper-v 拡張可能スイッチのデータパスを通過する各パケットの[ **\_NET BUFFER\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造には、帯域外 (OOB) データが含まれています。 このデータは、パケットの発信元ポート、およびパケット配信用の1つ以上の宛先ポートを指定します。 この OOB データは、*拡張可能なスイッチ転送コンテキスト*と呼ばれます。

このセクションでは、拡張可能なスイッチ転送コンテキストに関する次のトピックについて説明します。

[Hyper-v 拡張可能スイッチ転送コンテキストデータ型](hyper-v-extensible-switch-forwarding-context-data-types.md)

[Hyper-v 拡張可能スイッチの転送コンテキストの管理](managing-the-hyper-v-extensible-switch-forwarding-context.md)

 

 





