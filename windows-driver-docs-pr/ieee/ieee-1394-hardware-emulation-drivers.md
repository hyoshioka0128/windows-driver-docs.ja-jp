---
title: IEEE 1394 ハードウェア エミュレーション ドライバー
description: IEEE 1394 ハードウェア エミュレーション ドライバー
ms.assetid: 44141072-e425-4983-9234-3ad79daa2017
keywords:
- IEEE 1394 WDK バス、エミュレーション ドライバー
- 1394 WDK バス、エミュレーション ドライバー
- エミュレーション ドライバー WDK IEEE 1394 バス
- ハードウェア エミュレーション ドライバー WDK IEEE 1394 バス
- Pdo WDK IEEE 1394 バス
- 仮想 Pdo WDK の IEEE 1394 バス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5e00227bc9cc9b2252f19b55bbd39f989974bd2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532009"
---
# <a name="ieee-1394-hardware-emulation-drivers"></a>IEEE 1394 ハードウェア エミュレーション ドライバー





エミュレーション ドライバーは、システムの構成 ROM. に単位のディレクトリを追加することで実際の IEEE ハードウェアをエミュレートすることができます。 エミュレーション ドライバーでは、外部のノードからの要求をインターセプトし、実際のハードウェア デバイスによって公開されている、1394 レジスタをエミュレートします。

Microsoft では、ベンダーがエミュレーション ドライバーを実装するために使用する仮想デバイスのメカニズムを提供します。

仮想デバイスを作成する方法については、次を参照してください。[仮想デバイスの作成の IEEE 1394](https://msdn.microsoft.com/library/windows/hardware/ff537065)します。

仮想デバイスを削除する方法については、次を参照してください。[仮想デバイスを削除する IEEE 1394](https://msdn.microsoft.com/library/windows/hardware/ff537630)します。

少数の例外を除き、エミュレーション ドライバーは、実際のデバイスの機能のドライバーと同じ方法で完全な 1394 DDI を使用できます。 実数部と仮想デバイスを使用して、1394 DDI 方法の違いの詳細については、次を参照してください。[仮想デバイス ドライバーの IEEE 1394 をサポートしている要求](https://msdn.microsoft.com/library/windows/hardware/ff538825)します。

 

 




