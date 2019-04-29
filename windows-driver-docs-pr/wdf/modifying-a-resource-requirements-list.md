---
title: リソース要件リストの変更
description: リソース要件リストの変更
ms.assetid: 75391dd2-5ae1-4562-97a0-4de21a08b61c
keywords:
- ハードウェア リソース WDK KMDF、リソース要件の一覧を変更します。
- リソース要件の一覧を変更する、WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 065df4ec43703467b19c8ce6fd714d103c18e002
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390131"
---
# <a name="modifying-a-resource-requirements-list"></a>リソース要件リストの変更


PnP マネージャーことを確認するすべての新しく接続したデバイスのドライバーの後に読み込まれているデバイスのドライバー スタックに、デバイスのハードウェア要件の一覧を送信します。

一覧は、下位のスタック移動、フレームワークの各関数とフィルター ドライバーの[ *EvtDeviceFilterRemoveResourceRequirements* ](https://msdn.microsoft.com/library/windows/hardware/ff540872)としてハードウェア要件の一覧を渡すことのコールバック関数入力引数。 このコールバック関数では、バス ドライバーが指定したが、その関数のドライバーでは、デバイスが動作するために必要でないかを決定します。 ハードウェアの要件の一覧から、ハードウェア リソースを削除できます。

たとえば、PCI バス ドライバー レプリケート場合があります、PCI の仕様に従ってメモリ領域で、I/O 領域リソース。 デバイスは、I/O の領域のリソースを使用してなくても動作できます、デバイスの機能のドライバーは、ハードウェア要件の一覧から I/O 容量のリソースを削除できます。

要件の一覧から項目を削除するには、ドライバーは、次の操作を行うことができます。

-   リソース要件の一覧で論理構成を変更する次のメソッドを呼び出します。
    -   [**WdfIoResourceRequirementsListGetCount**](https://msdn.microsoft.com/library/windows/hardware/ff548545)を論理構成の数を取得します。
    -   [**WdfIoResourceRequirementsListGetIoResList**](https://msdn.microsoft.com/library/windows/hardware/ff548553)を論理構成へのアクセスを取得します。
    -   [**WdfIoResourceRequirementsListRemove** ](https://msdn.microsoft.com/library/windows/hardware/ff548570)と[ **WdfIoResourceRequirementsListRemoveByIoResList**](https://msdn.microsoft.com/library/windows/hardware/ff548575)、論理構成を削除します。
-   論理構成内でリソースの記述子を変更するのには、次のメソッドを呼び出します。
    -   [**WdfIoResourceListGetCount**](https://msdn.microsoft.com/library/windows/hardware/ff548506)リソースの記述子の数を取得します。
    -   [**WdfIoResourceListGetDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff548510)をリソース記述子へのアクセスを取得します。
    -   [**WdfIoResourceListRemove** ](https://msdn.microsoft.com/library/windows/hardware/ff548523)と[ **WdfIoResourceListRemoveByDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff548528)リソースの記述子を削除します。

一覧は、ドライバー スタックのバックアップを移動、フレームワークの各関数とフィルター ドライバーの[ *EvtDeviceFilterAddResourceRequirements* ](https://msdn.microsoft.com/library/windows/hardware/ff540870)コールバック関数をハードウェア要件入力引数としてリストされます。 このコールバック関数は、デバイスを操作する関数のドライバーを必要とする追加のハードウェア リソースを追加できます。

ハードウェア要件の一覧に項目を追加するには、ドライバーは、次の操作を行うことができます。

-   リソース要件の一覧で論理構成を変更する次のメソッドを呼び出します。
    -   [**WdfIoResourceRequirementsListGetCount**](https://msdn.microsoft.com/library/windows/hardware/ff548545)を論理構成の数を取得します。
    -   [**WdfIoResourceRequirementsListGetIoResList**](https://msdn.microsoft.com/library/windows/hardware/ff548553)を論理構成へのアクセスを取得します。
    -   [**WdfIoResourceListCreate**](https://msdn.microsoft.com/library/windows/hardware/ff548502)、新しい論理構成を作成します。
    -   [**WdfIoResourceRequirementsListAppendIoResList** ](https://msdn.microsoft.com/library/windows/hardware/ff548537)または[ **WdfIoResourceRequirementsListInsertIoResList**](https://msdn.microsoft.com/library/windows/hardware/ff548560)、新しい論理構成を追加します。
-   論理構成内でリソースの記述子を変更するのには、次のメソッドを呼び出します。
    -   [**WdfIoResourceListGetCount**](https://msdn.microsoft.com/library/windows/hardware/ff548506)リソースの記述子の数を取得します。
    -   [**WdfIoResourceListGetDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff548510)をリソース記述子へのアクセスを取得します。
    -   [**WdfIoResourceListAppendDescriptor** ](https://msdn.microsoft.com/library/windows/hardware/ff548498)または[ **WdfIoResourceListInsertDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff548513)リソース記述子を追加します。

 

 





