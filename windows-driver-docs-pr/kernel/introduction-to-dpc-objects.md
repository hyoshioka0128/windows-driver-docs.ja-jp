---
title: DPC オブジェクトの概要
description: DPC オブジェクトの概要
ms.assetid: ae8758f5-0e23-4db2-9eac-aab31d98247b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 31ae581000856c1d8b51d4d5ffc7ab8d7a150299
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341037"
---
# <a name="introduction-to-dpc-objects"></a>DPC オブジェクトの概要





Isr を特定可能な限り早く実行する必要があります、ため、ドライバーは通常 ISR 返します後まで、割り込みを処理の完了を延期する必要があります。 そのため、システムはサポートを提供します*遅延プロシージャ呼び出し*(Dpc) は、Isr からキューと isr よりも低いかどうかと、後で実行される。

各 DPC がシステム定義に関連付けられて*DPC オブジェクト*します。 システムでは、デバイス オブジェクトごとに 1 つの DPC オブジェクトを提供します。 ドライバーと呼ばれる DPC ルーチンの登録時に、システムはこの DPC オブジェクトを初期化します、 [ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)ルーチン。 ドライバーは、1 つ以上の DPC が必要な場合、追加の DPC オブジェクトを作成できます。 これらの余分な Dpc と呼ばれます。 [ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972)ルーチン。

ドライバーによって DPC オブジェクトの内容は直接参照されない必要があります。 オブジェクトの構造が記載されていません。 ドライバーでは、各デバイス オブジェクトに割り当てられたシステム提供の DPC オブジェクトへのアクセスはありません。 ドライバーの余分な Dpc、記憶域の割り当てが、これらの DPC オブジェクトの内容は、システム ルーチンのみが参照する必要があります。

DPC オブジェクトと Dpc は、タイマーにも使用できます。 詳細については、次を参照してください。[タイマー オブジェクトと Dpc](timer-objects-and-dpcs.md)します。

 

 




