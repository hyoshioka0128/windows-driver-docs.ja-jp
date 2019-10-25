---
title: DPC キューの編成
description: DPC キューの編成
ms.assetid: df176a6d-d7a7-4d8b-ab1b-fd7f5b89fcbe
keywords:
- DPC キュー WDK カーネル
- WDK DPC をキューに置いて
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3ba36b279b3d7b794991a6e9a3b5634dc83cf3b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838523"
---
# <a name="organization-of-dpc-queues"></a>DPC キューの編成


システムは、プロセッサごとに1つの DPC キューを提供します。 ドライバーは、システムが DPC を割り当てるキュー、キュー内の DPC の場所、およびキューが処理されるタイミングを制御できます。

特定のプロセッサのキューに割り当てられている Dpc は、そのプロセッサ上で実行されます。 既定では、ドライバーが[**KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc)または[**IoRequestDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdpc)を呼び出すと、現在アクティブなプロセッサで DPC がキューに置かれます。 ドライバーは、 **KeInsertQueueDpc**または**IoRequestDpc**を呼び出す前に[**Kesettargetprocessordpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kesettargetprocessordpc)を呼び出すことで、プロセッサキューを指定できます。

Windows Vista 以降のバージョンの Windows では、システムにはプロセッサごとに1つのスレッド DPC キューもあります。 ドライバーは**Kesettargetprocessordpc**を使用して、スレッド化された dpc のプロセッサキューを指定できます。

[**Kesetimportの dpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kesetimportancedpc)ルーチンは、キュー内の dpc が配置される場所を制御します。 通常、DPC はキューの最後に配置されます。ただし、優先*順位*パラメーターが**highimportance**と等しい場合、ドライバーは最初に**kesetimportの dpc**を呼び出しますが、DPC はキューの先頭に配置されます。

通常の (非スレッド) Dpc の場合、 **KesetimportKeInsertQueueDpc dpc**は、 dpc キューの処理を直ちに開始するかどうかも決定します。 キューを処理するための規則を次に示します。

-   Dpc キューの処理は、DPC が現在のプロセッサに割り当てられていて、*重要度*が**LowImportance**と等しくない場合、または*重要度*が**LowImportance**で、現在の dpc キューの深さに等しい場合に、すぐに開始されます。プロセッサがシステムで定義された制限を超えているか、DPC 要求率がシステムで定義されている最小値を下回っています。 そうしないと、適切なキューの深さとレートの要件が満たされるまで DPC の処理が遅延されます。

-   Dpc が現在のプロセッサに割り当てられている場合、dpc キューの処理はターゲットプロセッサですぐに開始されます。 DPC が現在のプロセッサとは異なるプロセッサに割り当てられ、*重要度*が**MediumHighImportance**または**highimportance**である場合、または dpcターゲットプロセッサのキューの深さが、システムで定義されている制限を超えています。 そうしないと、適切なキューの深さとレートの要件が満たされるまで DPC の処理が遅延されます。

 

 




