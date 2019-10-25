---
title: リソース要件リストの変更
description: リソース要件リストの変更
ms.assetid: 75391dd2-5ae1-4562-97a0-4de21a08b61c
keywords:
- ハードウェアリソース WDK KMDF、リソース要件リストの変更
- リソース要件の一覧 WDK KMDF、変更
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9439d9b28b6553bc2f8deaeb2aa7da3b463672c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843141"
---
# <a name="modifying-a-resource-requirements-list"></a>リソース要件リストの変更


PnP マネージャーは、新しく接続されたすべてのデバイスのドライバーが読み込まれたことを確認した後、デバイスのハードウェア要件リストをデバイスのドライバースタックに送信します。

リストがスタックをたどると、フレームワークは各関数とフィルタードライバーの[*EvtDeviceFilterRemoveResourceRequirements*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements) callback 関数を呼び出し、ハードウェア要件リストを入力引数として渡します。 このコールバック関数は、バスドライバーによって指定されたハードウェア要件の一覧からハードウェアリソースを削除できますが、デバイスを操作するために関数ドライバーによって決定される必要はありません。

たとえば、pci バスドライバーが PCI 仕様に従って、メモリ領域に i/o 領域リソースをレプリケートする場合があります。 I/o space リソースを使用せずにデバイスを動作させることができる場合は、デバイスの機能ドライバーによって、ハードウェア要件の一覧から i/o 領域リソースが削除されることがあります。

要件一覧から項目を削除するために、ドライバーは次の操作を実行できます。

-   次のメソッドを呼び出して、リソース要件の一覧の論理構成を変更します。
    -   [**WdfIoResourceRequirementsListGetCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcerequirementslistgetcount)。論理構成の数を取得します。
    -   [**WdfIoResourceRequirementsListGetIoResList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcerequirementslistgetioreslist)。論理構成へのアクセスを取得します。
    -   [**WdfIoResourceRequirementsListRemove**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcerequirementslistremove)と[**WdfIoResourceRequirementsListRemoveByIoResList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcerequirementslistremovebyioreslist)で、論理構成を削除します。
-   論理構成内のリソース記述子を変更するには、次のメソッドを呼び出します。
    -   [**WdfIoResourceListGetCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcelistgetcount)。リソース記述子の数を取得します。
    -   [**Wdfioresourcelistgetdescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcelistgetdescriptor)。リソース記述子へのアクセス権を取得します。
    -   [**Wdfioresourcelistremove**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcelistremove)および[**Wdfioresourcelistremovebydescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcelistremovebydescriptor)。リソース記述子を削除します。

リストがドライバースタックをさかのぼっていくにつれて、フレームワークは各関数とフィルタードライバーの[*EvtDeviceFilterAddResourceRequirements*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nc-wdffdo-evt_wdf_device_filter_resource_requirements) callback 関数を呼び出し、ハードウェア要件リストを入力引数として渡します。 このコールバック関数では、デバイスを動作させるために関数ドライバーが必要とするハードウェアリソースを追加できます。

ハードウェア要件の一覧に項目を追加するために、ドライバーは次の操作を実行できます。

-   次のメソッドを呼び出して、リソース要件の一覧の論理構成を変更します。
    -   [**WdfIoResourceRequirementsListGetCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcerequirementslistgetcount)。論理構成の数を取得します。
    -   [**WdfIoResourceRequirementsListGetIoResList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcerequirementslistgetioreslist)。論理構成へのアクセスを取得します。
    -   [**Wdfioresourcelistcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcelistcreate)。新しい論理構成を作成します。
    -   [**WdfIoResourceRequirementsListAppendIoResList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcerequirementslistappendioreslist)または[**WdfIoResourceRequirementsListInsertIoResList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcerequirementslistinsertioreslist)を追加して、新しい論理構成を追加します。
-   論理構成内のリソース記述子を変更するには、次のメソッドを呼び出します。
    -   [**WdfIoResourceListGetCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcelistgetcount)。リソース記述子の数を取得します。
    -   [**Wdfioresourcelistgetdescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcelistgetdescriptor)。リソース記述子へのアクセス権を取得します。
    -   [**Wdfioresourcelistappenddescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcelistappenddescriptor)または[**Wdfioresourcelistappenddescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcelistinsertdescriptor)。リソース記述子を追加します。

 

 





