---
title: 標準イベント オブジェクト
description: 標準イベント オブジェクト
ms.assetid: 3c34c485-28b1-45d5-9e79-05dd2b26015e
keywords:
- イベント オブジェクトの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97852e867c4fc3c2e66b17f201d93b320da2a09f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382999"
---
# <a name="standard-event-objects"></a>標準イベント オブジェクト





システムでは、いくつかの標準的なイベント オブジェクトを提供します。 ドライバーは、これらのイベント オブジェクトを使用して、特定の条件が発生するたびに、システムで通知します。 次の一覧には、標準的なイベント オブジェクトが含まれています。

<a href="" id="-kernelobjects-highmemorycondition"></a> **\\KernelObjects\\HighMemoryCondition**  
このイベントは、空き物理メモリの量は、システム定義の量を超えた場合に設定されます。 ドライバーは、積極的にメモリを割り当てできるように設定するには、このイベントで待機できます。

<a href="" id="-kernelobjects-lowmemorycondition"></a> **\\KernelObjects\\LowMemoryCondition**  
このイベントは、物理メモリの空き容量がシステム定義の量を下回るときに設定されます。 大量のメモリが割り当てられているドライバーは、未使用のメモリを解放するシグナルとして設定するには、このイベントで待機できます。

Microsoft Windows Server 2003 と Windows の以降のバージョンでは、ドライバーは、次の追加の標準的なイベント オブジェクトも使用できます。

<a href="" id="-kernelobjects-highpagedpoolcondition"></a> **\\KernelObjects\\HighPagedPoolCondition**  
このイベントは、無料のページ プールの容量がシステム定義の量を超えた場合に設定されます。 ドライバーを積極的にメモリを割り当てるページ プールからのシグナルとして設定するには、このイベントを待機できます。

<a href="" id="-kernelobjects-lowpagedpoolcondition"></a> **\\KernelObjects\\LowPagedPoolCondition**  
このイベントは、無料のページ プールの容量がシステム定義の量を下回るときに設定されます。 大量のメモリが割り当てられているドライバーは、ページ プールから未使用のメモリを解放するシグナルとして設定するには、このイベントで待機できます。

<a href="" id="-kernelobjects-highnonpagedpoolcondition"></a> **\\KernelObjects\\HighNonPagedPoolCondition**  
このイベントは、無料の非ページ プールの容量がシステム定義の量を超えた場合に設定されます。 ドライバーは、非ページ プールから積極的にメモリを割り当てできるように設定するには、このイベントで待機できます。

<a href="" id="-kernelobjects-lownonpagedpoolcondition"></a> **\\KernelObjects\\LowNonPagedPoolCondition**  
このイベントは、無料の非ページ プールの容量がシステム定義の量を下回るときに設定されます。 大量のメモリが割り当てられているドライバーを非ページ プールから未使用のメモリを解放するシグナルとして設定するには、このイベントを待機できます。

Windows Vista と Windows の以降のバージョンでは、ドライバーは、次の追加の標準的なイベント オブジェクトも使用できます。

<a href="" id="-kernelobjects-lowcommitcondition"></a> **\\KernelObjects\\LowCommitCondition**  
場合、このイベントが設定、オペレーティング システムの*コミット チャージ*はに対して相対的に低い、*現在のコミット制限*します。 つまり、メモリ使用率が低いと、物理メモリまたはページング ファイルに多くの領域があります。

<a href="" id="-kernelobjects-highcommitcondition"></a> **\\KernelObjects\\HighCommitCondition**  
このイベントは、オペレーティング システムのコミット チャージが高い場合、現在のコミット制限の基準としたときに設定されます。 つまり、メモリ使用率が高いと物理メモリのページング ファイルの場合は、ほとんどの空き領域があるが、オペレーティング システムのページング ファイルのサイズを大きくできる可能性があります。

<a href="" id="-kernelobjects-maximumcommitcondition"></a> **\\KernelObjects\\MaximumCommitCondition**  
このイベントは、オペレーティング システムのコミット チャージが近い場合は設定、*最大コミット制限*します。 つまり、メモリ使用量が非常に高い、非常に小さい領域が物理メモリのページング ファイル、およびオペレーティング システムのページング ファイルのサイズを増やすことはできません。 (システム管理者常に増やせますサイズや数、ページング ファイルのための十分な記憶域リソースが存在しない場合、コンピューターを再起動しなくても。)

これらの各イベントは、通知イベントです。 これらは、トリガーの条件が true として設定されたままです。

これらのイベントのいずれかを識別するハンドルを開くを使用して、 [ **IoCreateNotificationEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatenotificationevent)ルーチン。 これらのイベントのいずれかを待機するドライバーには、待機を実行する専用のスレッドを作成する必要があります。 いずれかを呼び出すことによってこれらのイベントの 1 つ以上のスレッドを待機できます[ **kewaitforsingleobject の 1** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)または[ **KeWaitForMultipleObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitformultipleobjects)します。

 

 




