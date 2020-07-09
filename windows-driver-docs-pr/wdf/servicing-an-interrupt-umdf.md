---
title: 割り込みの処理 (UMDF 1)
description: 割り込みの処理
ms.assetid: 79BA75B3-E10F-4AC1-A2C5-A502BF821188
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b70a4890494814ce597e9867561cd7e03567dc7
ms.sourcegitcommit: f788aa204a3923f9023d8690488459a4d9bc2495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86141267"
---
# <a name="servicing-an-interrupt-umdf-1"></a>割り込みの処理 (UMDF 1)


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

割り込みのサービスは、次の2つの手順で構成されます。

1.  中断サービスルーチンでの揮発性情報 (レジスタの内容など) の迅速な保存。
2.  作業項目ルーチンでの保存された volatile 情報の処理。

デバイスがハードウェア割り込みを生成すると、フレームワークは、ドライバーの interrupt service ルーチン (ISR) を呼び出します。これは、フレームワークベースのドライバーが[*OnInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_isr)コールバック関数として実装します。

[*OnInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_isr) callback 関数は、パッシブレベルで実行されます。これに \_ より、レジスタの内容、データを処理するための作業項目をキューに格納し、その割り込み回線が共有されている場合に、他の割り込みのサービスを可能にするために ISR から戻る必要があります。 UMDF ドライバーの ISR はパッシブレベルで実行 \_ されるため、PCI ラインベースの割り込みを処理することはお勧めしません。 これらの割り込みは、通常、複数のデバイス間で共有されますが、その中には ISR の遅延を受け入れることができないものもあります。 ただし、UMDF ドライバーで PCI MSI 割り込みを処理することはできます。 これらの割り込みはエッジセマンティクスを持ち、共有されていません。

通常、 [*OnInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_isr) callback 関数は、後で保存された情報を処理する作業項目をスケジュールします。 フレームワークベースのドライバーは、作業項目ルーチンを[*OnInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_workitem)コールバック関数として実装します。

ほとんどのドライバーでは、割り込みの種類ごとに1つの[*OnInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_workitem)コールバック関数を使用します。 *OnInterruptWorkItem*コールバック関数の実行をスケジュールするには、ドライバーが[*OnInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_isr) Callback 関数内から[**Iwdfinterrupt:: queueworkitemforisr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-queueworkitemforisr)を呼び出す必要があります。

ドライバーが各デバイスに対して複数のフレームワークキューオブジェクトを作成する場合は、キューごとに個別の workitem オブジェクトと[*Onworkitem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfworkitem/nc-wudfworkitem-wudf_workitem_function)コールバック関数を使用することを検討してください。 *Onworkitem*コールバック関数の実行をスケジュールするには、ドライバーがまず、ドライバーの[**Idriverentry:: ondeviceadd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)コールバック関数から[**IWdfDevice3:: createworkitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-createworkitem)を呼び出して1つ以上の作業項目オブジェクトを作成する必要があります。 次に、ドライバーの[*OnInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_isr) callback 関数は、 [**Iwdfworkitem:: エンキュー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfworkitem-enqueue)を呼び出すことができます。

ドライバーは通常、 [*OnInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_workitem)または[*onworkitem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfworkitem/nc-wudfworkitem-wudf_workitem_function)コールバック関数で i/o 要求を完了します。

割り込みを処理する UMDF ドライバーの例については、Windows 8 WDK から入手できる[SpbAccelerometer](https://go.microsoft.com/fwlink/p/?linkid=256189)サンプルドライバーを参照してください。

 

 





