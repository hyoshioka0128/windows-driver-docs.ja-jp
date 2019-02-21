---
title: IPsec のフレームの分割
description: IPsec のフレームの分割
ms.assetid: 2d6841f2-6eb6-4c59-80fb-5c777fa2bf56
keywords:
- WDK のネットワー キング、IPsec のフレームを分割するイーサネット フレーム
- WDK のネットワークを分割する IPsec フレーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8eb1da0a1a376ba1884d14c2f919449dd9f4b22
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537064"
---
# <a name="splitting-ipsec-frames"></a>IPsec のフレームの分割

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]




NIC で IPsec フレームに分割できます、[上のレイヤー プロトコル ヘッダーの先頭](splitting-frames-at-the-beginning-of-the-upper-layer-protocol-headers.md)、 [TCP ペイロードの先頭](splitting-frames-at-the-tcp-payload.md)、または[UDP ペイロードの先頭](splitting-frames-at-the-udp-payload.md)します。 NIC が IPsec 情報と同様に処理オプションの IPv4 または IPv6 拡張ヘッダー。

NIC はできない場合、結果のヘッダーのバッファーがある最大ヘッダー サイズより大きい長さフレームを分割することがあります。 ヘッダーの最大サイズの詳細については、次を参照してください。[ヘッダーのバッファーを割り当てる](allocating-the-header-buffer.md)します。

 

 





