---
title: Windows NT 4.0 SCSI ミニポートの変換プラグアンドプレイの概要
description: Windows NT 4.0 SCSI ミニポートの変換プラグアンドプレイの概要
ms.assetid: 46e5eb41-ff41-4054-856b-cc32f286e543
keywords:
- SCSI ミニポートドライバー WDK 記憶域、PnP
- PnP WDK SCSI
- WDK SCSI のプラグアンドプレイ
- SCSI ミニポートドライバーの変換
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2590249a6f28d2f0ebe2bad129dad4bb88e184c
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606556"
---
# <a name="converting-a-windows-nt-40-scsi-miniport-for-plug-and-play-overview"></a>Windows NT 4.0 SCSI ミニポートの変換プラグアンドプレイの概要

ミニポートドライバーによってプラグアンドプレイが有効になっている場合でも、ドライバーは初期化中にエラーが発生します。ただし、 *HwContext*ポインターと、ポートドライバーによって提供されるリソースの使用には特定の制限がありません。 また、ドライバーの予測可能な初期化順序に依存している場合は、初期化中にミニポートドライバーでエラーが発生することもあります。

プラグアンドプレイで正常に実行するには、次のセクションで説明するように、Microsoft Windows NT 4.0 ミニポートドライバーのソースコードを変更する必要がある場合があります。
