---
title: DPC キューの構造
description: DPC キューの構造
ms.assetid: df176a6d-d7a7-4d8b-ab1b-fd7f5b89fcbe
keywords:
- DPC キュー WDK カーネル
- WDK の DPC キュー
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a029b2f141c35f69949dd833b326ae57d626c751
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384919"
---
# <a name="organization-of-dpc-queues"></a>DPC キューの構造


システムでは、プロセッサごとに 1 つの DPC キューを提供します。 ドライバーは、DPC、DPC、キュー内の場所をシステムが割り当てられますがキューに登録し、キューを処理するときのコントロール。

特定のプロセッサのキューに割り当てられている Dpc は、そのプロセッサで実行されます。 ドライバーを呼び出すと、既定で[ **KeInsertQueueDpc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertqueuedpc)または[ **IoRequestDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iorequestdpc)DPC は現在アクティブなプロセッサのキューに配置します。 ドライバーは、呼び出すことによって、プロセッサのキューを指定できます[ **KeSetTargetProcessorDpc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-kesettargetprocessordpc)呼び出す前に**KeInsertQueueDpc**または**IoRequestDpc**.

Windows Vista および Windows の以降のバージョンでは、システムはプロセッサごとに 1 つのスレッド DPC キューもあります。 ドライバーを使用できる**KeSetTargetProcessorDpc**スレッド Dpc のプロセッサのキューを指定します。

[ **KeSetImportanceDpc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-kesetimportancedpc) DPC がキュー内に配置されているルーチン コントロール。 通常、DPC は; キューの末尾に配置されます。ドライバーを最初に呼び出す場合、 **KeSetImportanceDpc**で、*重要度*パラメーターと等しい**HighImportance**DPC はキューの先頭に置かれます。

通常の (非スレッドの) Dpc の**KeSetImportanceDpc**も決定するかどうか**KeInsertQueueDpc**または**IoRequestDpc** DPC の処理をすぐに開始されますキューです。 次の一覧には、キューを処理するための規則について説明します。

-   DPC の処理キューが直ちに開始すると、現在のプロセッサ、DPC が割り当てられている場合と*重要度*が等しくない**LowImportance**、または*重要度*は等しい**LowImportance** DPC 要求レートがシステム定義の最小値以下に低下や、現在のプロセッサの DPC キューの深さがシステム定義の制限を超えています。 それ以外の場合、DPC の処理は、適切なキューの深さとレートの要件が満たされるまで遅延されます。

-   DPC の処理キューが直ちに開始ターゲット プロセッサでは、現在のプロセッサを異なるプロセッサを DPC が割り当てられている場合と*重要度*equals **MediumHighImportance**または**HighImportance**ターゲットのプロセッサの DPC キューの深さがシステム定義の制限を超えた場合またはします。 それ以外の場合、DPC の処理は、適切なキューの深さとレートの要件が満たされるまで遅延されます。

 

 




