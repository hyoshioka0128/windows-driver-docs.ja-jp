---
title: DPC オブジェクトの概要
description: DPC オブジェクトの概要
ms.assetid: ae8758f5-0e23-4db2-9eac-aab31d98247b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a07943c5a620ff57f51de078729ed9b45af01848
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828227"
---
# <a name="introduction-to-dpc-objects"></a>DPC オブジェクトの概要





Isr は可能な限り迅速に実行する必要があるため、通常、ドライバーは、ISR が戻るまで割り込みのサービスの完了を延期する必要があります。 このため、システムでは*遅延プロシージャ呼び出し*(dpc) がサポートされています。 dpc は、isr からキューに配置できます。これは、後で ISR と低い IRQL で実行されます。

各 DPC は、システム定義の*dpc オブジェクト*に関連付けられています。 システムは、デバイスオブジェクトごとに1つの DPC オブジェクトを提供します。 [*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)ルーチンと呼ばれる dpc ルーチンがドライバーによって登録されると、システムによってこの dpc オブジェクトが初期化されます。 複数の DPC が必要な場合、ドライバーは追加の DPC オブジェクトを作成できます。 これらの追加 Dpc は[*customdpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)ルーチンと呼ばれます。

DPC オブジェクトの内容は、ドライバーによって直接参照されることはできません。 オブジェクトの構造は記載されていません。 ドライバーは、各デバイスオブジェクトに割り当てられたシステム指定の DPC オブジェクトにアクセスできません。 ドライバーは、追加の Dpc 用にストレージを割り当てますが、これらの DPC オブジェクトの内容は、システムルーチンによってのみ参照される必要があります。

DPC オブジェクトと Dpc は、タイマーでも使用できます。 詳細については、「 [Timer オブジェクトと dpc](timer-objects-and-dpcs.md)」を参照してください。

 

 




