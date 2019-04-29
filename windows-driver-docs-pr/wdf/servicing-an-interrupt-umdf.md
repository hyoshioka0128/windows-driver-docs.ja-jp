---
title: 割り込みの処理
description: 割り込みの処理
ms.assetid: 79BA75B3-E10F-4AC1-A2C5-A502BF821188
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9dc6865d3c35eb8d4f6b041a09ab8a84106f4350
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325158"
---
# <a name="servicing-an-interrupt"></a>割り込みの処理


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

割り込みのサービスは、2 つの手順で構成されます。

1.  割り込みサービス ルーチンのレジスタの内容) などの揮発性の情報を迅速に保存しています。
2.  作業項目のルーチンで保存された揮発性の情報を処理します。

どのフレームワーク ベースのドライバーの実装として、ドライバーの割り込みサービス ルーチン (ISR) フレームワークをデバイスでは、ハードウェア割り込みを生成するとき、 [ *OnInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/hh463902)コールバック関数。

[ *OnInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/hh463902)パッシブで実行されるコールバック関数\_レベル、する必要があります、レジスタの内容など、割り込みの情報を保存する簡単にキューにさらに、データを処理する作業項目その他の割り込みの割り込みの行が共有されている場合を処理できる ISR から返します。 UMDF ドライバーの ISR はパッシブで実行されるため\_レベル、PCI 行ベースの割り込みの処理はお勧めしません。 通常、これらの割り込みは、ISR 遅延を受け入れない場合の複数のデバイス間で共有されます。 ただし、UMDF ドライバーでは、PCI MSI 割り込みを処理できます。 これらの割り込みは、edge のセマンティクスを持つし、は共有されません。

通常、 [ *OnInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/hh463902)コールバック関数は、後で保存された情報を処理する作業項目をスケジュールします。 フレームワーク ベースのドライバーとして作業項目のルーチンを実装する[ *OnInterruptWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/hh463905)コールバック関数。

ほとんどのドライバーを使用して、1 つ[ *OnInterruptWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/hh463905)割り込みの種類ごとのコールバック関数。 実行をスケジュールする、 *OnInterruptWorkItem*コールバック関数、ドライバーを呼び出す必要があります[ **IWDFInterrupt::QueueWorkItemForIsr** ](https://msdn.microsoft.com/library/windows/hardware/hh451314)内から、 [*OnInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/hh463902)コールバック関数。

ドライバーは、各デバイスのキュー オブジェクトは複数のフレームワークを作成する場合は、個別の作業項目オブジェクトを使用してを検討する可能性がありますと[ *OnWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/hh463909)キューごとのコールバック関数。 実行をスケジュールする、 *OnWorkItem*コールバック関数を呼び出して、ドライバーは 1 つ以上の作業項目オブジェクトを作成する必要がありますまず[ **IWdfDevice3::CreateWorkItem**](https://msdn.microsoft.com/library/windows/hardware/hh451213)、通常は、ドライバーから[ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)コールバック関数。 ドライバーの[ *OnInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/hh463902)コールバック関数を呼び出すことができます[ **IWDFWorkItem::Enqueue**](https://msdn.microsoft.com/library/windows/hardware/hh463883)します。

ドライバーは、通常の I/O 要求を完了、 [ *OnInterruptWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/hh463905)または[ *OnWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/hh463909)コールバック関数。

割り込みを処理する UMDF ドライバーの例は、次を参照してください。、 [SpbAccelerometer](https://go.microsoft.com/fwlink/p/?linkid=256189)サンプル ドライバー、以降、Windows 8 WDK で使用できます。

 

 





