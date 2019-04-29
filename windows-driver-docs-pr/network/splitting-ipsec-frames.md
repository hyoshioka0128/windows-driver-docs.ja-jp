---
title: IPsec フレームの分割
description: IPsec フレームの分割
ms.assetid: 2d6841f2-6eb6-4c59-80fb-5c777fa2bf56
keywords:
- WDK のネットワー キング、IPsec のフレームを分割するイーサネット フレーム
- WDK のネットワークを分割する IPsec フレーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8eb1da0a1a376ba1884d14c2f919449dd9f4b22
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392897"
---
# <a name="splitting-ipsec-frames"></a>IPsec フレームの分割

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]




NIC で IPsec フレームに分割できます、[上のレイヤー プロトコル ヘッダーの先頭](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)、 [TCP ペイロードの先頭](splitting-frames-at-the-tcp-payload.md)、または[UDP ペイロードの先頭](splitting-frames-at-the-udp-payload.md)します。 NIC が IPsec 情報と同様に処理オプションの IPv4 または IPv6 拡張ヘッダー。

NIC はできない場合、結果のヘッダーのバッファーがある最大ヘッダー サイズより大きい長さフレームを分割することがあります。 ヘッダーの最大サイズの詳細については、次を参照してください。[ヘッダーのバッファーを割り当てる](allocating-the-header-buffer.md)します。

 

 





