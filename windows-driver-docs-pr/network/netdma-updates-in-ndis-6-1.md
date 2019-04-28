---
title: NDIS 6.1 で NetDMA 更新プログラム
description: NDIS 6.1 で NetDMA 更新プログラム
ms.assetid: ec19ac6e-78b3-4da5-baef-e02fc9947c0e
keywords:
- NetDMA インターフェイスの詳細については、ネットワーク NetDMA WDK
ms.date: 01/09/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6fad15a17d85a824db12bb4817ac89401e1a7e99
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369886"
---
# <a name="netdma-updates-in-ndis-61"></a>NDIS 6.1 で NetDMA 更新プログラム

>[!IMPORTANT]
> Windows 8 以降、NetDMA インターフェイスがサポートされていません。

NetDMA DMA エンジンをサポートするダイレクト メモリ アクセス (DMA) をネットワーク インターフェイス カード (Nic) のオフロード NetDMA インターフェイスを提供します。 Windows Server 2008 および Windows Vista Service Pack 1 (SP1) オペレーティング システムでは、NetDMA version 1.1 および 2.0 を追加します。 NDIS 6.1 と以降のドライバーは、NetDMA バージョン 1.0、1.1、2.0 インターフェイスを使用できます。 これらのインターフェイスは、DMA エンジンとの対話を管理し、実行時に DMA の転送を管理します。

NetDMA インターフェイスは、Nic とその他のドライバーに対して提供されている省略可能なサービスです。

NetDMA の詳細については、次を参照してください。 [NetDMA ドライバー](netdma-drivers.md)します。