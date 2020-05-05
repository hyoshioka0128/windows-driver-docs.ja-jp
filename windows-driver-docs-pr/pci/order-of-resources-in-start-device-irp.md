---
title: 開始デバイス IRP でのリソースの順序
description: 開始デバイス IRP でのリソースの順序
ms.assetid: df55105e-3da3-40cc-9f57-05632cb2d043
keywords:
- リソースの順序 (WDK PCI)
- 開始-デバイスの IRP WDK PCI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fba7bee0e267206fa246f8b3bdf35a1618aae21
ms.sourcegitcommit: 49d7f27a24360559456063092ac35b2ba1aba7b1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2020
ms.locfileid: "82742614"
---
# <a name="order-of-resources-in-start-device-irp"></a>開始デバイス IRP でのリソースの順序

開始デバイス i/o 要求パケット (IRP) で報告されるリソースの順序は、PCI ベースアドレスレジスタ (バー) に示されているリソースの順序と一致している必要があります。 リソースリストには、未加工と翻訳の2種類があります。 各リソースリストにはリソース記述子があります。 リソースリスト内のリソース記述子は、PCI デバイス上のベースアドレスレジスタ (バー) の順序になっています。 未加工および翻訳済みリスト内のリソースの順序は同じです。 2つの連続するリソース記述子の間にデバイスプライベート記述子データがあります。 バーのリソース記述子には、拡張メッセージシグナル割り込み (MSI-X) メッセージの1つまたは複数の記述子、MSI 用の1つの記述子、またはハードウェアベースの割り込み用の1つ以上の記述子が続きます。 たとえば、ビデオデバイスの場合など、場合によっては、バーの記述子の後に、従来のビデオリソースの記述子が続きます。 リソースリスト内のバーの記述子の順序は、すべてのハードウェアプラットフォーム上の PCI デバイス上のバーと一致することが保証されています。
