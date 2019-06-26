---
title: 多機能オーディオ デバイス
description: 多機能オーディオ デバイス
ms.assetid: 6ef54b12-d0ea-4e55-afee-61f834375b92
keywords:
- WDM オーディオ ドライバー WDK、多機能デバイス
- オーディオ ドライバー WDK、多機能デバイス
- WDK 多機能オーディオ デバイス
- サブデバイス WDK オーディオ
- 多機能オーディオ デバイス WDK、多機能のオーディオ デバイスについて
- 複数の関数オーディオ デバイス WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fd48264f0cd614ea5d57a50d807be937363e191
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355344"
---
# <a name="multifunction-audio-devices"></a>多機能オーディオ デバイス


## <span id="multifunction_audio_devices"></span><span id="MULTIFUNCTION_AUDIO_DEVICES"></span>


多機能デバイスは、2 つ以上個別関数 (またはサブデバイス) が組み込まれている 1 つのアダプター カードです。 多機能デバイスには、2 つ以上のオーディオ サブデバイスを含めることができます。 デバイス クラスにもわたる可能性があります。 オーディオとモデムのサブデバイスを格納しているデバイスは、たとえば、メディアのクラスとモデム クラスの両方に属しています。 詳細については、次を参照してください。[多機能デバイスをサポートしている](https://docs.microsoft.com/windows-hardware/drivers/multifunction/index)します。

PortCls で WavePci ポート ドライバーは、特別な要件を多機能デバイスに配置します。 具体的には、アダプターのドライバーでは、多機能デバイスで他のサブデバイスとは独立して制御できるように、各サブデバイスを構成する方法を提供する必要があります。 これは、2 つの方法のいずれかで多機能デバイスの PCI 構成領域を設定して実行できます。

1.  各論理的に区別サブデバイス多機能デバイス上に別のデバイス ID を割り当てることをお勧めします。 システムが、独立した devnode でとして各サブデバイスを表すできる多機能デバイスが含まれる場合、モデム、オーディオ、およびジョイスティック サブデバイス、たとえば、[デバイス ツリー](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-tree)します。 各デバイス ID で表されるサブデバイスは、独自の PCI レジスタのセットを備え、直交して、その他のサブデバイスの独立したは。 たとえば、有効化または 1 つサブデバイス (、オーディオ サブデバイス、たとえば) を無効にするないはず他サブデバイス (たとえばモデム) への影響です。 この種類の多機能デバイス自体サブデバイスの独自のドライバーとは別の特殊なハードウェア固有のドライバー サポートは不要です。

2.  多機能デバイスを設計するの 2 つ目の方法、デバイス全体に 1 つのデバイス ID を割り当てると、個別の PCI ベース アドレス個々 サブデバイス (棒) の登録を提供することです。 は、レジスタの共通セットを共有する、サブデバイスが各サブデバイス独自バーまたはバーです。 システムの多機能ドライバー (たとえば、 *Mf.sys* Microsoft Windows 2000 以降; を参照してください[System-Supplied 多機能バス ドライバーを使用して](https://docs.microsoft.com/windows-hardware/drivers/multifunction/using-the-system-supplied-multifunction-bus-driver)) 各ベース アドレスを構成することができます。サブデバイスの状態、コマンド、およびデータは、その他の関数のレジスタとは無関係に登録します。 デバイスのバーがサブデバイスによって論理的に分離できる場合は、PortCls を使用してデバイスを管理することはできません。

このセクションの残りの部分では、上記のリスト (2) のアプローチを実装するために必要な手順について説明します。 次のトピックについて説明します。

[複数のオーディオ サブデバイス](multiple-audio-subdevices.md)

[多機能デバイスの制限](multifunction-device-limits.md)

 

 




