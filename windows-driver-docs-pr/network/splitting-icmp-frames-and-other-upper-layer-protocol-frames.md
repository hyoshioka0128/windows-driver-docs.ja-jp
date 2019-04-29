---
title: ICMP フレームとその他の上位層プロトコル フレームの分割
description: ICMP フレームとその他の上位層プロトコル フレームの分割
ms.assetid: 693c0b23-f9b5-4a1e-a6c7-5f658a9a636c
keywords:
- WDK のネットワークを分割 ICMP フレーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b075000e83f42526b843d41a022a7beb1e4c9120
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392896"
---
# <a name="splitting-icmp-frames-and-other-upper-layer-protocol-frames"></a>ICMP フレームとその他の上位層プロトコル フレームの分割





NIC は、TCP または UDP (たとえば、ICMP フレーム) 上のレイヤー プロトコル ヘッダーの先頭以外の上のレイヤーのプロトコルを持つ IP フレームに分割する必要があります。 または、このようなフレームを分割する必要があります。

上のレイヤー プロトコル ヘッダーを分割の詳細については、次を参照してください。[上のレイヤー プロトコル ヘッダーの先頭のフレームの分割](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)します。

 

 





