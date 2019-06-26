---
title: リソース要件リストの変更
description: リソース要件リストの変更
ms.assetid: 75391dd2-5ae1-4562-97a0-4de21a08b61c
keywords:
- ハードウェア リソース WDK KMDF、リソース要件の一覧を変更します。
- リソース要件の一覧を変更する、WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4a9a1a5639b67a1264c5536dffd1b8cb0570d33
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376657"
---
# <a name="modifying-a-resource-requirements-list"></a>リソース要件リストの変更


PnP マネージャーことを確認するすべての新しく接続したデバイスのドライバーの後に読み込まれているデバイスのドライバー スタックに、デバイスのハードウェア要件の一覧を送信します。

一覧は、下位のスタック移動、フレームワークの各関数とフィルター ドライバーの[ *EvtDeviceFilterRemoveResourceRequirements* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)としてハードウェア要件の一覧を渡すことのコールバック関数入力引数。 このコールバック関数では、バス ドライバーが指定したが、その関数のドライバーでは、デバイスが動作するために必要でないかを決定します。 ハードウェアの要件の一覧から、ハードウェア リソースを削除できます。

たとえば、PCI バス ドライバー レプリケート場合があります、PCI の仕様に従ってメモリ領域で、I/O 領域リソース。 デバイスは、I/O の領域のリソースを使用してなくても動作できます、デバイスの機能のドライバーは、ハードウェア要件の一覧から I/O 容量のリソースを削除できます。

要件の一覧から項目を削除するには、ドライバーは、次の操作を行うことができます。

-   リソース要件の一覧で論理構成を変更する次のメソッドを呼び出します。
    -   [**WdfIoResourceRequirementsListGetCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcerequirementslistgetcount)を論理構成の数を取得します。
    -   [**WdfIoResourceRequirementsListGetIoResList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcerequirementslistgetioreslist)を論理構成へのアクセスを取得します。
    -   [**WdfIoResourceRequirementsListRemove** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcerequirementslistremove)と[ **WdfIoResourceRequirementsListRemoveByIoResList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcerequirementslistremovebyioreslist)、論理構成を削除します。
-   論理構成内でリソースの記述子を変更するのには、次のメソッドを呼び出します。
    -   [**WdfIoResourceListGetCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcelistgetcount)リソースの記述子の数を取得します。
    -   [**WdfIoResourceListGetDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcelistgetdescriptor)をリソース記述子へのアクセスを取得します。
    -   [**WdfIoResourceListRemove** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcelistremove)と[ **WdfIoResourceListRemoveByDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcelistremovebydescriptor)リソースの記述子を削除します。

一覧は、ドライバー スタックのバックアップを移動、フレームワークの各関数とフィルター ドライバーの[ *EvtDeviceFilterAddResourceRequirements* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements)コールバック関数をハードウェア要件入力引数としてリストされます。 このコールバック関数は、デバイスを操作する関数のドライバーを必要とする追加のハードウェア リソースを追加できます。

ハードウェア要件の一覧に項目を追加するには、ドライバーは、次の操作を行うことができます。

-   リソース要件の一覧で論理構成を変更する次のメソッドを呼び出します。
    -   [**WdfIoResourceRequirementsListGetCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcerequirementslistgetcount)を論理構成の数を取得します。
    -   [**WdfIoResourceRequirementsListGetIoResList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcerequirementslistgetioreslist)を論理構成へのアクセスを取得します。
    -   [**WdfIoResourceListCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcelistcreate)、新しい論理構成を作成します。
    -   [**WdfIoResourceRequirementsListAppendIoResList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcerequirementslistappendioreslist)または[ **WdfIoResourceRequirementsListInsertIoResList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcerequirementslistinsertioreslist)、新しい論理構成を追加します。
-   論理構成内でリソースの記述子を変更するのには、次のメソッドを呼び出します。
    -   [**WdfIoResourceListGetCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcelistgetcount)リソースの記述子の数を取得します。
    -   [**WdfIoResourceListGetDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcelistgetdescriptor)をリソース記述子へのアクセスを取得します。
    -   [**WdfIoResourceListAppendDescriptor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcelistappenddescriptor)または[ **WdfIoResourceListInsertDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfresource/nf-wdfresource-wdfioresourcelistinsertdescriptor)リソース記述子を追加します。

 

 





