---
title: 動的な列挙
description: 動的な列挙
ms.assetid: 6e46b456-7d2d-4c6e-8692-7f310366387d
keywords:
- 動的列挙型 WDK KMDF
- 子の説明 WDK KMDF
- アドレスの説明 WDK KMDF
- WDK KMDF の識別の説明
- 動的な子リスト WDK KMDF
- 動的な子リストの走査 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cd974a90c06dc9e3ff447acd4c30b96e9d45eff
ms.sourcegitcommit: a54b96c52b0c7009dfa05bcc68d210b13711f2ea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/25/2020
ms.locfileid: "77601722"
---
# <a name="dynamic-enumeration"></a>動的な列挙


*動的列挙*は、システムの実行中にシステムに接続されているデバイスの数と種類に対する変更を検出して報告するためのドライバーの機能です。

親デバイスに接続されているデバイスの数または種類がシステムの構成によって異なる場合、バスドライバーは動的列挙を使用する必要があります。 これらのデバイスの中には、常にシステムに接続されているものと、システムの実行中に接続が切断されているものがあります。

たとえば、システムの PCI バスに接続されているデバイスの数と種類はシステムに依存しますが、ユーザーが電源をオフにした場合は永続的な状態になります。また、ドライバーを使用してデバイスを追加または削除しない限り、永続的になります。 一方、ユーザーは、システムの実行中にケーブルを接続または取り外して、USB デバイスを追加または削除できます。

### <a name="dynamic-child-lists"></a>動的な子リスト

フレームワークの子リストオブジェクトを提供することで、ドライバーが動的列挙をサポートできるようになります。 各子リストオブジェクトは、親デバイスに接続されている子デバイスの一覧を表します。 親デバイスのバスドライバーは、親の子デバイスを識別し、親デバイスの子リストに追加して、各子の物理デバイスオブジェクト (PDO) を作成する必要があります。

デバイスの FDO を表すフレームワークデバイスオブジェクトがドライバーによって作成されるたびに、フレームワークによって、デバイスの空の既定の子リストが作成されます。 ドライバーは、 [**WdfFdoGetDefaultChildList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdogetdefaultchildlist)を呼び出すことによって、デバイスの既定の子リストへのハンドルを取得できます。 通常、デバイスの子を列挙するバスドライバーを作成する場合、ドライバーは子を既定の子リストに追加できます。 追加の子リストを作成する必要がある場合は、ドライバーが[**Wdfchildlistcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistcreate)を呼び出すことができます。

ドライバーが子リストを使用できるようにするには、その前に子リストオブジェクトを構成する必要があります。そのためには、 [**WDF\_子\_リスト\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/ns-wdfchildlist-_wdf_child_list_config)構造体を初期化し、その構造体を[**Wdffdoinitsetdefaultchildlistconfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitsetdefaultchildlistconfig)、既定の子リスト、または[**wdfchildlistcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistcreate)に渡します。

### <a name="dynamic-child-descriptions"></a>動的な子の説明

バスドライバーが子デバイスを識別するたびに、子デバイスの説明を子リストに追加する必要があります。 *子の説明*は、必須の*識別の説明*とオプションのアドレスの*説明*で構成されます。

<a href="" id="identification-description"></a>*識別の説明*  
識別の説明は、ドライバーが列挙する各デバイスを一意に識別する情報を含む構造体です。 ドライバーはこの構造体を定義しますが、その最初のメンバーは[ **\_子\_識別\_説明\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/ns-wdfchildlist-_wdf_child_identification_description_header)構造体である必要があります。

通常、id の説明には、デバイスの[デバイス識別文字列](https://docs.microsoft.com/windows-hardware/drivers/install/device-identification-strings)、場合によってはシリアル番号、バス上のデバイスの場所に関する情報 (スロット番号など) が含まれます。

ドライバーは、次のコールバック関数のセットを提供できます。これにより、フレームワークは識別の説明の情報を操作できます。

-   [*EvtChildListIdentificationDescriptionCompare*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_identification_description_compare)。2つの識別記述構造体の内容を比較します。

-   [*EvtChildListIdentificationDescriptionCopy*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_identification_description_copy)。識別説明の構造体の内容を別のものにコピーします。

-   [*EvtChildListIdentificationDescriptionDuplicate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_identification_description_duplicate)。既存の識別説明の構造を複製して新しい識別の説明を作成し、必要に応じて追加のバッファーを割り当てます。

-   [*EvtChildListIdentificationDescriptionCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_identification_description_cleanup)。 [*EvtChildListIdentificationDescriptionDuplicate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_identification_description_duplicate) callback 関数によって割り当てられたバッファーを解放します。

通常、ドライバーの識別記述構造に動的に割り当てられたバッファーへのポインターが含まれている場合は、これらのコールバック関数を提供する必要があります。 これらのコールバック関数の目的の詳細については、参照ページを参照してください。

<a href="" id="address-description"></a>*アドレスの説明*  
アドレスの説明は、デバイスが接続されている間に情報が変更される可能性がある場合に、バス上のデバイスにアクセスするためにドライバーが必要とする情報を含む構造体です。 この構造はドライバーで定義されていますが、その最初のメンバーは、 [**WDF\_子\_ADDRESS\_DESCRIPTION\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/ns-wdfchildlist-_wdf_child_address_description_header)構造体である必要があります。

アドレスの説明は省略可能です。 デバイスが接続されている時間とデバイスが取り外された時間の間でデバイスのアドレス情報が変更されない場合は、デバイスのすべてのアドレス情報を識別の説明に保存できます。 たとえば、USB コントローラーは、デバイスが接続されているときにデバイスにアドレスを割り当てます。これらのアドレスは変更されません。

一方、一部のバスでは、変更可能なアドレス指定情報が使用されます。 たとえば、IEEE 1394 バスでは、"生成数" を使用します。これは、発生したバスリセットの数です。 IEEE 1394 デバイスに対する各非同期 i/o 要求には、生成数を含める必要があります。 このアドレス情報は変更される可能性があるため、ドライバーはアドレスの説明に保存する必要があります。

ドライバーは、アドレスの説明の情報を操作するために、次のコールバック関数のセットを提供できます。

-   [*Evtchildlistaddressdescriptioncopy*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_address_description_copy)。1つのアドレス説明構造の内容を別のアドレス記述構造にコピーします。

-   [*Evtchildlistaddressdescriptionduplicate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_address_description_duplicate)。既存のアドレス記述構造を複製して新しいアドレスの説明を作成し、必要に応じて追加のバッファーを割り当てます。

-   [*Evtchildlistaddressdescriptioncleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_address_description_cleanup)。 [*Evtchildlistaddressdescriptioncleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_address_description_duplicate)コールバック関数によって割り当てられたバッファーを解放します。

通常、ドライバーのアドレス記述構造に動的に割り当てられたバッファーへのポインターが含まれている場合は、これらのコールバック関数を提供する必要があります。 これらのコールバック関数の目的の詳細については、参照ページを参照してください。

### <a name="adding-devices-to-a-dynamic-child-list"></a>動的な子リストへのデバイスの追加

フレームワークがバスドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数を呼び出す場合、コールバック関数は[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出して親デバイスの FDO を作成する必要があります。これは通常、バスアダプターです。 FDO の作成の詳細については、「[関数ドライバーでのデバイスオブジェクトの作成](creating-device-objects-in-a-function-driver.md)」を参照してください。 次に、ドライバーは親デバイスの子を列挙し、子リストに子を追加する必要があります。

必要に応じて、ドライバーは[**WdfDeviceSetBusInformationForChildren**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetbusinformationforchildren)を呼び出して、バスに関する情報をフレームワークに提供できます。 これを行うことをお勧めします。これにより、子デバイスとアプリがバスを識別しやすくなります。

子リストに子を追加するには、ドライバーが検出した子デバイスごとに[**WdfChildListAddOrUpdateChildDescriptionAsPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistaddorupdatechilddescriptionaspresent)を呼び出す必要があります。 この呼び出しは、親デバイスに接続されている子デバイスがドライバーによって検出されたことをフレームワークに通知します。 ドライバーが**WdfChildListAddOrUpdateChildDescriptionAsPresent**を呼び出すと、id の説明と、必要に応じてアドレスの説明が提供されます。

ドライバーが[**WdfChildListAddOrUpdateChildDescriptionAsPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistaddorupdatechilddescriptionaspresent)を呼び出して新しいデバイスを報告した後、新しいデバイスが存在することを PnP マネージャーに通知します。 PnP マネージャーは、新しいデバイスのデバイススタックとドライバースタックを構築します。 このプロセスの一環として、フレームワークはバスドライバーの[*EvtChildListCreateDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device)コールバック関数を呼び出します。 このコールバック関数は、 [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出して、新しいデバイス用の PDO を作成する必要があります。

通常、いくつかの子デバイスは親に接続されているため、バスドライバーは[**WdfChildListAddOrUpdateChildDescriptionAsPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistaddorupdatechilddescriptionaspresent)を複数回呼び出す必要があります。 これを行う最も効率的な方法は次のとおりです。

1.  [**Wdfchildlistbeginscan**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistbeginscan)を呼び出します。

2.  各子デバイスの[**WdfChildListAddOrUpdateChildDescriptionAsPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistaddorupdatechilddescriptionaspresent)を呼び出します。

3.  [**Wdfchildlistendscan**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistendscan)を呼び出します。

[**Wdfchildlistbeginscan**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistbeginscan)および[**wdfchildlistbeginscan**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistendscan)の呼び出しを使用してドライバーの動的列挙を囲むと、フレームワークはすべての変更を子リストに格納し、ドライバーが**wdfchildlistbeginscan**を呼び出したときに、変更の PnP マネージャーに通知します。 後で、フレームワークは、子リスト内の各デバイスに対してバスドライバーの[*EvtChildListCreateDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_create_device) callback 関数を呼び出します。 このコールバック関数は、 [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出して、新しいデバイスごとに PDO を作成します。

ドライバーが[**Wdfchildlistbeginscan**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistbeginscan)を呼び出すと、フレームワークは以前に報告されたすべてのデバイスを存在しないとマークします。 そのため、ドライバーは、新たに検出された子だけでなく、ドライバーが検出できるすべての子に対して[**WdfChildListAddOrUpdateChildDescriptionAsPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistaddorupdatechilddescriptionaspresent)を呼び出す必要があります。 子リストに1つの子を追加する場合、ドライバーは最初に**Wdfchildlistbeginscan**を呼び出さずに[**WdfChildListUpdateAllChildDescriptionsAsPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistupdateallchilddescriptionsaspresent)を1回呼び出すことができます。

### <a name="updating-a-dynamic-child-list"></a>動的な子リストの更新

動的な子リストの情報を更新するには、次の2つの一般的な方法があります。

1.  親デバイスが子の到着または削除を示す割り込みを受け取ると、ドライバーの[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) callback 関数は、デバイスが接続されている場合は[**WdfChildListAddOrUpdateChildDescriptionAsPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistaddorupdatechilddescriptionaspresent)を、デバイスが取り外されていない場合は[**WdfChildListUpdateChildDescriptionAsMissing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistupdatechilddescriptionasmissing)を呼び出します。

2.  ドライバーは[*Evtchildlistscanforchildren*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nc-wdfchildlist-evt_wdf_child_list_scan_for_children)コールバック関数を提供できます。この関数は、親デバイスが動作 (D0) 状態になるたびにフレームワークによって呼び出されます。 このコールバック関数は、 [**Wdfchildlistbeginscan**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistbeginscan)、 [**WdfChildListAddOrUpdateChildDescriptionAsPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistaddorupdatechilddescriptionaspresent) (または[**WdfChildListUpdateAllChildDescriptionsAsPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistupdateallchilddescriptionsaspresent))、および[**wdfchildlistbeginscan**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistendscan)を呼び出すことにより、すべての子デバイスを列挙する必要があります。

ドライバーでは、これらの方法のいずれかまたは両方を使用できます。

### <a name="traversing-a-dynamic-child-list"></a>動的な子リストの走査

ドライバーで子リストの内容を確認する場合は、次のいずれかの方法を使用してリストを走査できます。

-   各子デバイスの説明の内容を一度に1つずつ取得するには、次のようにします。

    1.  [**Wdfchildlistbeginiteration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistbeginiteration)を呼び出します。
    2.  必要な回数だけ[**WdfChildListRetrieveNextDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistretrievenextdevice)を呼び出します。
    3.  [**Wdfchildlistenditeration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistenditeration)呼び出します。

    [**Wdfchildlistbeginiteration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistbeginiteration)を呼び出すと、ドライバーは、フレームワークがすべてのデバイスの説明を取得する必要があるか、またはサブセットのみを取得する必要があるかを示す、 [ **\_子\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/ne-wdfchildlist-_wdf_retrieve_child_flags)型のフラグを取得\_を指定します。 [**WdfChildListRetrieveNextDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistretrievenextdevice)が一致を検出すると、子デバイスの識別とアドレスの説明、およびデバイスオブジェクトへのハンドルを取得します。

-   子デバイスの説明に現在含まれているアドレスの説明を取得する必要がある場合、ドライバーは識別の説明を指定して[**WdfChildListRetrieveAddressDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistretrieveaddressdescription)を呼び出すことができます。 フレームワークは、id の説明が一致する子デバイスが見つかるまで子リストを走査し、アドレスの説明を取得します。

-   特定の子デバイスに関連付けられているフレームワークデバイスオブジェクトへのハンドルを取得する必要がある場合、ドライバーは[**WdfChildListRetrievePdo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfchildlist/nf-wdfchildlist-wdfchildlistretrievepdo)を呼び出すことができます。 フレームワークは、id の説明が一致する子デバイスが見つかるまで子リストを走査し、デバイスオブジェクトハンドルを返します。

### <a name="accessing-a-pdos-identification-and-address-descriptions"></a>PDO の Id とアドレスの説明へのアクセス

ドライバーは、次のメソッドを呼び出して、PDO の識別説明またはアドレスの説明にアクセスできます。

-   [**WdfPdoRetrieveIdentificationDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoretrieveidentificationdescription): PDO に関連付けられている識別の説明を取得します。

-   [**WdfPdoRetrieveAddressDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoretrieveaddressdescription): PDO に関連付けられているアドレスの説明を取得します。

-   [**WdfPdoUpdateAddressDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoupdateaddressdescription): PDO に関連付けられているアドレスの説明を更新します。

### <a name="handling-re-enumeration-requests"></a>再列挙要求の処理

動的列挙をサポートするフレームワークベースのバスドライバーは、 [**REENUMERATE_SELF_INTERFACE_STANDARD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_reenumerate_self_interface_standard)インターフェイスを介して特定の子デバイスを reenumerate するための要求を受け取ることができます。 詳細については、「[列挙型要求の処理](https://docs.microsoft.com/windows-hardware/drivers/wdf/handling-enumeration-requests)」を参照してください。






