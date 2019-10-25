---
title: 標準イベント オブジェクト
description: 標準イベント オブジェクト
ms.assetid: 3c34c485-28b1-45d5-9e79-05dd2b26015e
keywords:
- イベントオブジェクト WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15b193d31288ae2c3c186604d11b1909bf0e9c03
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836245"
---
# <a name="standard-event-objects"></a>標準イベント オブジェクト





システムには、いくつかの標準イベントオブジェクトが用意されています。 ドライバーは、これらのイベントオブジェクトを使用して、特定の条件が発生するたびにシステムから通知を受けることができます。 次の一覧には、標準のイベントオブジェクトが含まれています。

<a href="" id="-kernelobjects-highmemorycondition"></a> **\\KernelObjects\\HighMemoryCondition**  
このイベントは、空き物理メモリの量がシステムで定義されている量を超えたときに設定されます。 ドライバーは、メモリを積極的に割り当てるために、このイベントがシグナルとして設定されるのを待機できます。

<a href="" id="-kernelobjects-lowmemorycondition"></a> **\\KernelObjects\\LowMemoryCondition**  
このイベントは、空き物理メモリの量がシステムで定義されている量を下回るたびに設定されます。 大量のメモリが割り当てられているドライバーは、このイベントがシグナルとして設定されるのを待って、未使用のメモリを解放することができます。

Microsoft Windows Server 2003 以降のバージョンの Windows では、ドライバーは次の追加の標準イベントオブジェクトも使用できます。

<a href="" id="-kernelobjects-highpagedpoolcondition"></a> **\\KernelObjects\\HighPagedPoolCondition**  
このイベントは、空きページプールの量がシステムで定義されている量を超えた場合に設定されます。 ドライバーは、ページングされたプールからメモリを積極的に割り当てるために、このイベントがシグナルとして設定されるのを待機できます。

<a href="" id="-kernelobjects-lowpagedpoolcondition"></a> **\\KernelObjects\\LowPagedPoolCondition**  
このイベントは、空きページプールの量がシステムで定義された量を下回るたびに設定されます。 大量のメモリが割り当てられているドライバーは、このイベントがポケットベルプールから未使用のメモリを解放するシグナルとして設定されるのを待機できます。

<a href="" id="-kernelobjects-highnonpagedpoolcondition"></a> **\\KernelObjects\\HighNonPagedPoolCondition**  
このイベントは、無料の非ページプールの量がシステムで定義されている量を超えた場合に設定されます。 ドライバーは、非ページプールからメモリを積極的に割り当てるために、このイベントがシグナルとして設定されるのを待機できます。

<a href="" id="-kernelobjects-lownonpagedpoolcondition"></a> **\\KernelObjects\\LowNonPagedPoolCondition**  
このイベントは、未使用の非ページプールの量がシステムで定義された量を下回るたびに設定されます。 大量のメモリが割り当てられているドライバーは、このイベントが非ページプールから未使用のメモリを解放するシグナルとして設定されるのを待機できます。

Windows Vista 以降のバージョンの Windows では、ドライバーは次の追加の標準イベントオブジェクトも使用できます。

<a href="" id="-kernelobjects-lowcommitcondition"></a> **\\KernelObjects\\LowCommitCondition**  
このイベントは、*現在のコミット制限*に対して、オペレーティングシステムの*コミットの料金*が低い場合に設定されます。 つまり、メモリ使用量が少なく、物理メモリまたはページングファイルで大量の領域が使用可能になっています。

<a href="" id="-kernelobjects-highcommitcondition"></a> **\\KernelObjects\\HighCommitCondition**  
このイベントは、現在のコミット制限に対して、オペレーティングシステムのコミットの料金が高い場合に設定されます。 つまり、メモリ使用量が多く、物理メモリまたはページングファイルで使用できる領域が非常に少なくなっていますが、オペレーティングシステムはページングファイルのサイズを増やすことができる可能性があります。

<a href="" id="-kernelobjects-maximumcommitcondition"></a> **\\KernelObjects\\MaximumCommitCondition**  
このイベントは、オペレーティングシステムのコミット料金が*最大コミット制限*に近づいている場合に設定されます。 つまり、メモリ使用量が非常に高く、物理メモリまたはページングファイルに使用できる領域が非常に少ないため、オペレーティングシステムはページングファイルのサイズを大きくできません。 (システム管理者は、十分な記憶域リソースが存在する場合は、コンピューターを再起動せずに、ページングファイルのサイズまたは数を常に増やすことができます)。

これらのイベントはそれぞれ、通知イベントです。 トリガー条件が true のままである限り、これらは設定されたままになります。

これらのイベントのいずれかへのハンドルを開くには、 [**IoCreateNotificationEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatenotificationevent)ルーチンを使用します。 これらのイベントのいずれかを待機するドライバーは、待機を行う専用のスレッドを作成する必要があります。 スレッドは、 [**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)または[**KeWaitForMultipleObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)のいずれかを呼び出すことによって、これらのイベントの1つ以上を待機できます。

 

 




