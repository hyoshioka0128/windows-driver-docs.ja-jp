---
title: IP のフレームをフラグメント化分割
description: IP のフレームをフラグメント化分割
ms.assetid: faee7ec8-a49e-4107-a83f-d97391d69b43
keywords:
- WDK のネットワーク、IP フレームが断片化を分割するイーサネット フレーム
- IP フレーム WDK のヘッダー データが断片化の分割します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8cb2b3c5cbe742aa30c0f4035dfe2a9234f5892
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560017"
---
# <a name="splitting-fragmented-ip-frames"></a>IP のフレームをフラグメント化分割





NIC があるフレームを分割する必要があります断片化 IP フレームにプロトコル レイヤー上のヘッダーが含まれている場合、[レイヤー プロトコルの上限ヘッダーの先頭](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)またはフレームを分割する必要があります。 NIC では、TCP または UDP ペイロードの先頭に IP フレームが断片化が分割されない必要があります。

断片化された IPv4 フレームにプロトコル レイヤー上のヘッダーが含まれていない場合、NIC は、UDP または TCP ペイロードの先頭のフレームに分割する必要があります。 またはフレームを分割する必要があります。

フラグメント化された IPv6 フレームにプロトコル レイヤー上のヘッダーが含まれていない場合、NIC は、フレームを分割する必要があります。

上のレイヤー プロトコル ヘッダーの先頭のフレームの分割の詳細については、[上のレイヤー プロトコル ヘッダーの先頭のフレームの分割](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)を参照してください。

 

 





