---
title: DPC オブジェクトの概要
description: DPC オブジェクトの概要
ms.assetid: ae8758f5-0e23-4db2-9eac-aab31d98247b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ad5796d121b085cd806c29894045608509c148d1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369768"
---
# <a name="introduction-to-dpc-objects"></a>DPC オブジェクトの概要





Isr を特定可能な限り早く実行する必要があります、ため、ドライバーは通常 ISR 返します後まで、割り込みを処理の完了を延期する必要があります。 そのため、システムはサポートを提供します*遅延プロシージャ呼び出し*(Dpc) は、Isr からキューと isr よりも低いかどうかと、後で実行される。

各 DPC がシステム定義に関連付けられて*DPC オブジェクト*します。 システムでは、デバイス オブジェクトごとに 1 つの DPC オブジェクトを提供します。 ドライバーと呼ばれる DPC ルーチンの登録時に、システムはこの DPC オブジェクトを初期化します、 [ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)ルーチン。 ドライバーは、1 つ以上の DPC が必要な場合、追加の DPC オブジェクトを作成できます。 これらの余分な Dpc と呼ばれます。 [ *CustomDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kdeferred_routine)ルーチン。

ドライバーによって DPC オブジェクトの内容は直接参照されない必要があります。 オブジェクトの構造が記載されていません。 ドライバーでは、各デバイス オブジェクトに割り当てられたシステム提供の DPC オブジェクトへのアクセスはありません。 ドライバーの余分な Dpc、記憶域の割り当てが、これらの DPC オブジェクトの内容は、システム ルーチンのみが参照する必要があります。

DPC オブジェクトと Dpc は、タイマーにも使用できます。 詳細については、次を参照してください。[タイマー オブジェクトと Dpc](timer-objects-and-dpcs.md)します。

 

 




