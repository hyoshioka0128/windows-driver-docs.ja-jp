---
title: デバイスとアダプターの初期化
description: デバイスとアダプターの初期化
ms.assetid: 394BDE67-2667-4672-896A-2407F3A54725
keywords:
- NetAdapterCx デバイスの初期化, NetCx デバイスの初期化, NetAdapterCx アダプターの初期化, NetCx アダプターの初期化
ms.date: 08/06/2018
ms.localizationpriority: medium
ms.openlocfilehash: f01841277202d0ae4c76c2f6d8d24c877f9713cf
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210814"
---
# <a name="managing-the-lifetime-of-objects-in-netadaptercx"></a>NetAdapterCx でのオブジェクトの有効期間の管理

ここでは、NetAdapterCx でのフレームワークオブジェクトとその有効期間について説明します。 これらのトピックを使用して、標準の[WDF オブジェクト](../wdf/wdf-objects.md)に加えて、ネットワーク固有のオブジェクトの詳細を確認し、それらを初期化、開始、停止、および破棄する方法についても説明します。

このセクションの内容

- [Summary of NetAdapterCx objects (NetAdapterCx オブジェクトの概要)](summary-of-netadaptercx-objects.md)
- [Device and adapter initialization (デバイスとアダプターの初期化)](device-and-adapter-initialization.md)
- [Power-up sequence for a NetAdapterCx client driver (NetAdapterCx クライアント ドライバーの電源投入シーケンス)](power-up-sequence-for-a-netadaptercx-client-driver.md)
- [Power-down sequence for a NetAdapterCx client driver (NetAdapterCx クライアント ドライバーの電源切断シーケンス)](power-down-sequence-for-a-netadaptercx-client-driver.md)
