---
title: Hyper-V 拡張可能スイッチ転送コンテキストの概要
description: Hyper-V 拡張可能スイッチ転送コンテキストの概要
ms.assetid: B2BF07B5-FA44-4994-9605-EFF4A0B9179F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9c817ef13e498bee0a781f49c1a3ff62b0d3559
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823892"
---
# <a name="hyper-v-extensible-switch-forwarding-context-overview"></a>Hyper-V 拡張可能スイッチ転送コンテキストの概要


Hyper-v 拡張可能スイッチのデータパスを通過する各パケットの[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造には、帯域外 (OOB) データが含まれています。 このデータは、パケットの発信元ポート、およびパケット配信用の1つ以上の宛先ポートを指定します。 この OOB データは、*拡張可能なスイッチ転送コンテキスト*と呼ばれます。

このセクションでは、拡張可能なスイッチ転送コンテキストに関する次のトピックについて説明します。

[Hyper-v 拡張可能スイッチ転送コンテキストデータ型](hyper-v-extensible-switch-forwarding-context-data-types.md)

[Hyper-v 拡張可能スイッチの転送コンテキストの管理](managing-the-hyper-v-extensible-switch-forwarding-context.md)

 

 





