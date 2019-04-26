---
title: 動的な列挙
description: 動的な列挙
ms.assetid: 6e46b456-7d2d-4c6e-8692-7f310366387d
keywords:
- WDK KMDF の動的な列挙型
- 子の説明 WDK KMDF
- WDK KMDF アドレスの説明
- WDK KMDF 識別の説明
- 動的な子 WDK KMDF を一覧表示します。
- 動的な子を走査 WDK KMDF を一覧表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fa6659f7cac4e5bd15aa28a1d7cdc07a47c3792
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342827"
---
# <a name="dynamic-enumeration"></a>動的な列挙


*動的な列挙*は検出し、システムの実行中に、システムに接続されているデバイスの種類と数に変更を報告するドライバーの機能です。

バス ドライバーは、数または親デバイスに接続されているデバイスの種類はシステムの構成に依存している場合、動的な列挙型を使用する必要があります。 これらのデバイスの一部のシステムに常に接続する可能性があり、いくつかに接続されているし、システムの実行中に電源が入っていない可能性があります。

たとえば、システムの PCI バスに接続されているデバイスの種類と数がシステムに依存するが、ユーザー電源をオフに、開く場合とを追加しますかドライバーを使用してデバイスを削除しない限り、永続的なは。 その一方で、ユーザーは追加または取り外しを行うシステムの実行中に、ケーブルを取り外すして USB デバイスを削除できます。

### <a name="dynamic-child-lists"></a>動的な子のリスト

フレームワークは、フレームワークの子リスト オブジェクトを提供することによって動的な列挙をサポートするドライバーを使用できます。 子リストの各オブジェクトは、親デバイスに接続されている子デバイスの一覧を表します。 親デバイス用のバス ドライバーでは、親の子のデバイスを識別、親デバイスの子の一覧に追加、およびそれぞれの子の物理デバイス オブジェクト (PDO) を作成する必要があります。

ドライバーが、デバイスの FDO を表す framework デバイス オブジェクトを作成するたびに、空の場合は、デバイスの既定の子リストに、フレームワークが作成されます。 ドライバーは呼び出すことによって、デバイスの既定の子のリストを識別するハンドルを取得することができます[ **WdfFdoGetDefaultChildList**](https://msdn.microsoft.com/library/windows/hardware/ff547235)します。 通常、このデバイスの子を列挙するバス ドライバーを作成する場合、ドライバーは既定の子リストに子を追加できます。 追加の子のリストを作成する必要がある場合、ドライバーを呼び出すことができます[ **WdfChildListCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545615)します。

初期化子リスト オブジェクトを構成する必要があります、ドライバーは、子リストを使用できます、前に、 [ **WDF\_子\_一覧\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551227)構造体を渡して、いずれかに構造[ **WdfFdoInitSetDefaultChildListConfig**](https://msdn.microsoft.com/library/windows/hardware/ff547258)、既定の子リスト、またはに[ **WdfChildListCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545615)、追加の子リスト。

### <a name="dynamic-child-descriptions"></a>動的な子の説明

バス ドライバーが、子デバイスを識別するたびに子リストに子デバイスの説明を追加する必要があります、します。 A*子説明*は、必須の*識別説明*は省略可能*説明に対処*。

<a href="" id="identification-description"></a>*識別の説明*  
識別の説明は、ドライバーを列挙する各デバイスを一意に識別する情報を含む構造です。 ドライバーは、この構造体を定義しますが、その最初のメンバーである必要があります、 [ **WDF\_子\_識別\_説明\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff551223)構造体。

通常、デバイスには識別の説明を[識別文字列](https://msdn.microsoft.com/library/windows/hardware/ff541224)、場合によっては、シリアル番号、およびスロット番号など、バス上のデバイスの場所に関する情報。

ドライバーは、次の一連のコールバック関数。 これにより、識別の説明の情報を操作するためにフレームワークを指定できます。

-   [*EvtChildListIdentificationDescriptionCompare*](https://msdn.microsoft.com/library/windows/hardware/ff540833)、2 つの識別の説明の構造体の内容が比較されています。

-   [*EvtChildListIdentificationDescriptionCopy*](https://msdn.microsoft.com/library/windows/hardware/ff540834)、別に 1 つの識別の説明の構造体の内容をコピーします。

-   [*EvtChildListIdentificationDescriptionDuplicate*](https://msdn.microsoft.com/library/windows/hardware/ff540836)、既存の id の説明の構造を複製し、必要に応じて、追加のバッファーを割り当てる新しい識別の説明を作成します。

-   [*EvtChildListIdentificationDescriptionCleanup*](https://msdn.microsoft.com/library/windows/hardware/ff540832)、によって割り当てられたバッファーの割り当てを解除する、 [ *EvtChildListIdentificationDescriptionDuplicate* ](https://msdn.microsoft.com/library/windows/hardware/ff540836)コールバック関数。

通常、ドライバーの識別の説明の構造体には、動的に割り当てられたバッファーへのポインターが含まれている場合は、これらのコールバック関数を提供する必要があります。 これらのコールバック関数の目的に関する詳細については、それらの参照ページを参照してください。

<a href="" id="address-description"></a>*アドレスの説明*  
アドレスの説明は、デバイスが接続中に情報を変更できる場合、そのバス上のデバイスにアクセスできるようにをドライバーが必要な情報を格納する構造体です。 ドライバーは、この構造体を定義しますが、その最初のメンバーである必要があります、 [ **WDF\_子\_アドレス\_説明\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff551219)構造体。

アドレスの説明は省略可能です。 デバイスが接続されている時刻とが接続されていない時刻の間をデバイスのアドレス情報を変更できない場合、識別の説明ですべてのデバイスのアドレス情報を格納できます。 たとえば、USB コント ローラーで、デバイスが接続されているし、これらのアドレスは変更しないでください、デバイスにアドレスを割り当てます。

その一方で、いくつかのバスは、変更可能なアドレス指定情報を使用します。 たとえば、IEEE 1394 バスが"生成数を使用、"はバスのリセットが発生した数。 IEEE 1394 デバイスへの非同期 I/O 要求ごとでは、生成数を含める必要があります。 このアドレス情報が変更できるので、ドライバーする必要がありますに保存、アドレスの説明。

ドライバーは、次の一連のアドレスの説明の情報を操作のコールバック関数を指定できます。

-   [*EvtChildListAddressDescriptionCopy*](https://msdn.microsoft.com/library/windows/hardware/ff540824)、別に 1 つのアドレスの説明の構造体の内容をコピーします。

-   [*EvtChildListAddressDescriptionDuplicate*](https://msdn.microsoft.com/library/windows/hardware/ff540826)、既存のアドレスの説明の構造を複製し、必要に応じて、追加のバッファーを割り当てる新しいアドレスの説明が作成されます。

-   [*EvtChildListAddressDescriptionCleanup*](https://msdn.microsoft.com/library/windows/hardware/ff540823)、によって割り当てられたバッファーの割り当てを解除する、 [ *EvtChildListAddressDescriptionDuplicate* ](https://msdn.microsoft.com/library/windows/hardware/ff540826)コールバック関数.

通常、ドライバーのアドレスの説明の構造体には、動的に割り当てられたバッファーへのポインターが含まれている場合は、これらのコールバック関数を提供する必要があります。 これらのコールバック関数の目的に関する詳細については、それらの参照ページを参照してください。

### <a name="adding-devices-to-a-dynamic-child-list"></a>動的な子の一覧にデバイスを追加

ときに、フレームワークがバス ドライバーの[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック関数では、コールバック関数を呼び出す必要があります[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)バス アダプターは、通常、親デバイスの FDO を作成します。 FDO の作成の詳細については、次を参照してください。 [Function ドライバーのデバイス オブジェクトの作成](creating-device-objects-in-a-function-driver.md)です。 ドライバーは、親デバイスの子を列挙する必要がありますし、子を子リストに追加します。

ドライバーを呼び出すことができます必要に応じて、 [ **WdfDeviceSetBusInformationForChildren** ](https://msdn.microsoft.com/library/windows/hardware/ff546868)バスについての情報をフレームワークを提供します。 子デバイスと、バスを識別するためにアプリを簡単になりますので、これをお勧めします。

子を子リストを追加するドライバーを呼び出す必要があります[ **WdfChildListAddOrUpdateChildDescriptionAsPresent** ](https://msdn.microsoft.com/library/windows/hardware/ff545591)検出された各子デバイス。 この呼び出しは、ドライバーが、親デバイスに接続されている子デバイスを検出されたことをフレームワークに通知します。 ドライバーを呼び出すと**WdfChildListAddOrUpdateChildDescriptionAsPresent**識別の説明と、必要に応じて、アドレスの説明を提供します。

ドライバーの呼び出し後[ **WdfChildListAddOrUpdateChildDescriptionAsPresent** ](https://msdn.microsoft.com/library/windows/hardware/ff545591)フレームワークを新しいデバイスを報告するには、新しいデバイスに存在する PnP マネージャーに通知します。 PnP マネージャーは、デバイス スタックと新しいデバイスのドライバー スタックを作成します。 このプロセスの一環として、フレームワークに呼び出す、バス ドライバーの[ *EvtChildListCreateDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540828)コールバック関数。 このコールバック関数を呼び出す必要があります[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)を新しいデバイスの PDO を作成します。

親、子のいくつかのデバイスが接続されているため、バス ドライバーを呼び出す必要が通常、 [ **WdfChildListAddOrUpdateChildDescriptionAsPresent** ](https://msdn.microsoft.com/library/windows/hardware/ff545591)何回か。 これを行うに最も効率的な方法は次のです。

1.  呼び出す[ **WdfChildListBeginScan**](https://msdn.microsoft.com/library/windows/hardware/ff545608)します。

2.  呼び出す[ **WdfChildListAddOrUpdateChildDescriptionAsPresent** ](https://msdn.microsoft.com/library/windows/hardware/ff545591)子デバイスごとにします。

3.  呼び出す[ **WdfChildListEndScan**](https://msdn.microsoft.com/library/windows/hardware/ff545626)します。

呼び出しで、ドライバーの動的な列挙を囲むかどうか[ **WdfChildListBeginScan** ](https://msdn.microsoft.com/library/windows/hardware/ff545608)と[ **WdfChildListEndScan**](https://msdn.microsoft.com/library/windows/hardware/ff545626)、フレームワークは、すべての子の一覧に変更を格納し、ドライバーを呼び出すと、変更の PnP マネージャーに通知**WdfChildListEndScan**します。 後で、フレームワーク、バス ドライバーの[ *EvtChildListCreateDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540828)子リスト内の各デバイスのコールバック関数。 このコールバック関数を呼び出す[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)を新しいデバイスごとの PDO を作成します。

ドライバーを呼び出すと[ **WdfChildListBeginScan**](https://msdn.microsoft.com/library/windows/hardware/ff545608)フレームワークが存在するとして以前に報告されたすべてのデバイスをマークします。 そのため、ドライバーを呼び出す必要があります[ **WdfChildListAddOrUpdateChildDescriptionAsPresent** ](https://msdn.microsoft.com/library/windows/hardware/ff545591)ドライバーを検出できるすべての子、子を検出しない新しくだけです。 に子のリストを 1 つの子を追加するドライバーが 1 回の呼び出しを行うことができます[ **WdfChildListUpdateAllChildDescriptionsAsPresent** ](https://msdn.microsoft.com/library/windows/hardware/ff545667)最初に呼び出さず**WdfChildListBeginScan**.

### <a name="updating-a-dynamic-child-list"></a>動的な子の一覧を更新しています

動的な子の一覧で情報を更新する 2 つの一般的な方法はあります。

1.  親デバイスが到達または子のドライバーの削除を示す、割り込みを受信すると[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)コールバック関数の呼び出し[ **WdfChildListAddOrUpdateChildDescriptionAsPresent** ](https://msdn.microsoft.com/library/windows/hardware/ff545591)デバイスが接続されている場合または[ **WdfChildListUpdateChildDescriptionAsMissing** ](https://msdn.microsoft.com/library/windows/hardware/ff545674)場合、デバイスの接続が解除されました。

2.  ドライバーが提供できる、 [ *EvtChildListScanForChildren* ](https://msdn.microsoft.com/library/windows/hardware/ff540838)フレームワークは、親デバイスがその作業 (D0) 状態になるたびに、コールバック関数。 このコールバック関数が呼び出すことによってすべての子デバイスを列挙する必要があります[ **WdfChildListBeginScan**](https://msdn.microsoft.com/library/windows/hardware/ff545608)、 [ **WdfChildListAddOrUpdateChildDescriptionAsPresent**](https://msdn.microsoft.com/library/windows/hardware/ff545591) (または[ **WdfChildListUpdateAllChildDescriptionsAsPresent**](https://msdn.microsoft.com/library/windows/hardware/ff545667))、および[ **WdfChildListEndScan** ](https://msdn.microsoft.com/library/windows/hardware/ff545626).

ドライバーでは、これらの手法の一方または両方を使用できます。

### <a name="traversing-a-dynamic-child-list"></a>動的な子リスト内の移動

子リストの内容を確認するには、ドライバーを実行する場合に、次の手法の 1 つを使用して、リストを走査、ことができます。

-   デバイスの説明を 1 つずつ、それぞれの子の内容を取得するには、ドライバーでは次のことができます。

    1.  呼び出す[ **WdfChildListBeginIteration**](https://msdn.microsoft.com/library/windows/hardware/ff545601)します。
    2.  呼び出す[ **WdfChildListRetrieveNextDevice**](https://msdn.microsoft.com/library/windows/hardware/ff545655)必要に応じて何度です。
    3.  呼び出す[ **WdfChildListEndIteration**](https://msdn.microsoft.com/library/windows/hardware/ff545618)します。

    呼び出すときに[ **WdfChildListBeginIteration**](https://msdn.microsoft.com/library/windows/hardware/ff545601)、ドライバーを指定します、 [ **WDF\_取得\_子\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/ff552507)-フレームワークですべてのデバイスの説明またはサブセットのみを取得する必要があるかどうかを示すフラグを入力します。 ときに[ **WdfChildListRetrieveNextDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff545655)一致を子デバイスの識別とアドレスの説明については、そのデバイス オブジェクトを識別するハンドルを取得します。

-   子デバイスの説明に現在格納されているアドレスの説明を取得する必要がある場合、ドライバーが呼び出せる[ **WdfChildListRetrieveAddressDescription**](https://msdn.microsoft.com/library/windows/hardware/ff545648)を指定して、識別の説明です。 フレームワークは、一致する識別の説明では、子デバイスを見つけたし、アドレスの説明を取得し、まで子リストを走査します。

-   特定の子デバイスに関連付けられている framework デバイス オブジェクトを識別するハンドルを取得する必要がある場合、ドライバーを呼び出すことができます[ **WdfChildListRetrievePdo**](https://msdn.microsoft.com/library/windows/hardware/ff545663)します。 フレームワークは、識別の説明、一致する子デバイスを見つけたし、デバイス オブジェクトのハンドルを返しますまで子リストを走査します。

### <a name="accessing-a-pdos-identification-and-address-descriptions"></a>PDO の識別とアドレスの説明へのアクセス

ドライバーは、PDO の識別またはアドレスの説明へのアクセスには、次のメソッドを呼び出すことができます。

-   [**WdfPdoRetrieveIdentificationDescription**](https://msdn.microsoft.com/library/windows/hardware/ff548824)PDO に関連付けられている識別の説明を取得します。

-   [**WdfPdoRetrieveAddressDescription**](https://msdn.microsoft.com/library/windows/hardware/ff548820)PDO に関連付けられているアドレスの説明を取得します。

-   [**WdfPdoUpdateAddressDescription**](https://msdn.microsoft.com/library/windows/hardware/ff548826)PDO に関連付けられているアドレスの説明を更新します。

 

 





