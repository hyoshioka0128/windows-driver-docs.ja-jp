---
title: ERESOURCE 構造体の概要
description: ERESOURCE 構造体の概要
ms.assetid: 5c7759db-aeb5-47f3-8adc-ddedb74b5cb4
keywords:
- ÷の構造体
- exclusive 待機処理 WDK カーネル
- shared 待機処理 WDK カーネル
- 排他的/共有同期 WDK カーネル
- 同期 WDK カーネル、排他/共有
- 待機処理 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f9575b485ef1d75c184f1f8e49033fba33135a1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838627"
---
# <a name="introduction-to-eresource-routines"></a>ERESOURCE 構造体の概要





システムには、現在の状態を確認するためだけでなく、作業中の構造体を取得して解放するルーチンが用意されています。

### <a name="acquiring-and-releasing-an-eresource-structure"></a>を取得し、この構造体を解放する

ドライバーは、使用して、*共有と共有の同期*を実装することができます。 排他的/共有同期は次のように機能します。

-   任意の数のスレッドが、共有として共有を取得できます。

-   1つのスレッドのみが、1つの資源を排他的に取得できます。 %1 は、まだ共有として取得されているスレッドがない場合にのみ取得できます。

現在の場合は、現在のスレッドを待機状態にすることができます。 システムは、2つのスレッドのリストを保持しています。これは、*待機処理*の一覧と*共有待機処理*のリストです。

排他的/共有同期の一般的な使用方法は、読み取り/書き込みロックを実装することです。 読み取り/書き込みロックでは、複数のスレッドで読み取り操作を実行できますが、一度に書き込むことができるスレッドは1つだけです。 これは、によって直接実装できます。

ドライバーは、資源のストレージを割り当て、 [**Exinitializer Eresourcelite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializeresourcelite)を使用して初期化します。 システムは、使用されているすべての÷の構造体の一覧を保持します。 ドライバーが特定の資源を必要としなくなった場合は、 [**ExDeleteResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeleteresourcelite)を呼び出してシステムの一覧から削除する必要があります。 また、ドライバーは、 [**Exreinitializer Eresourcelite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreinitializeresourcelite)を呼び出すことによって、資源を再利用することもできます。

ドライバーは、次の基本的な操作を実行できます。

-   [**ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)を使用して共有として共有を取得します。 このルーチンは、リソースが排他的に取得されておらず、排他的な待機処理がない場合にのみ、リソースを取得します。

-   [**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)を使用して、"%" を排他的に取得します。 このルーチンは、排他的にまたは共有として取得されていない限り、リソースを取得します。

-   [**ExConvertExclusiveToSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544558)を使用して、排他取得を共有取得に変換します。

-   [**ExReleaseResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite)を使用して、取得したリソースを解放します。

[**ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)と[**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)の*Wait*パラメーターによって、現在のスレッドが、現在のスレッドが使用されるのを待機しているかどうかが判断されます。 値を**false**に指定し、かつ、値を取得できない場合、ルーチンは**false**を返します。 値**TRUE**を指定した場合、現在のスレッドは、その値に対応する待機リストに配置されます。

### <a name="examining-the-state-of-an-eresource-structure"></a>の状態を調べています。

また、次のように、ドライバーは、現在の状態を確認することもできます。

-   [**ExIsResourceAcquiredLite**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545466(v=vs.85))または[**ExIsResourceAcquiredSharedLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite)を使用して、が既に shared または exclusive として取得されているかどうかを確認します。 [**ExIsResourceAcquiredExclusiveLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredexclusivelite)を使用して、指定されているときに、そのときに、このときには、このときにのみ。

-   ExGetExclusiveWaiterCount の共有待機処理の数を確認するには、 [**Exgetsharedwa count**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exgetsharedwaitercount)を使用します。また、待機処理の排他的の数を決定するには、 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exgetexclusivewaitercount)を使用します。

 

 




