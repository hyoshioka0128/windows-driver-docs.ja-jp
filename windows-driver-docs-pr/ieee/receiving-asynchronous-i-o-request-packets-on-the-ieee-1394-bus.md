---
title: IEEE 1394 バスでの非同期 I/O 要求パケットの受信
description: コンピューター自体は IEEE 1394 バス上のノードであるため、非同期 i/o 要求を受信できます。
ms.assetid: 7b8eaf40-7fdc-4c25-86a7-8377d2d51877
keywords:
- 非同期 i/o 要求の受信
- アドレス範囲の割り当て
- WDK IEEE 1394 バスに対応
- バッキングストア WDK IEEE 1394 バス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 020784e1aa5f377a41dd2774aa8d610fb7a52afd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841530"
---
# <a name="receiving-asynchronous-io-request-packets-on-the-ieee-1394-bus"></a>IEEE 1394 バスでの非同期 I/O 要求パケットの受信

コンピューター自体は IEEE 1394 バス上のノードであるため、非同期 i/o 要求を受信できます。 ドライバーは、コンピューターの IEEE 1394 アドレス空間にアドレスの範囲を割り当て、\_アドレス\_範囲の要求をバスドライバーに割り当てる\_要求を送信することによって、外部ノードから要求を受信します。

ドライバーは、アドレス範囲を割り当てるときに、デバイスが割り当てられたアドレスに送信できるトランザクションの種類を指定できます。そのためには、1つ以上のアクセス\_フラグ\_型\_読み取り、アクセス\_フラグ\_型\_要求の IRB の fulAccessType メンバーに\_ロック\_種類を書き込むか、アクセス\_フラグを**指定**します。 指定された種類のいずれでもない要求は自動的に失敗します。

2つの異なるドライバーが同じアドレス範囲を割り当てる場合があります。 既定では、バスドライバーは自動的に要求の多重化を解除し、ドライバーはドライバーのデバイスから割り当てられたアドレスの要求のみを認識します。 ドライバーは、バス上のすべてのノードによってアドレスに送信されたすべてのパケットを受信するように要求することができます。そのためには、 **fulAccessType**にアクセス\_フラグ\_種類\_ブロードキャストフラグを指定します。

* [割り当てられたアドレス](#allocated-addresses)
* [割り当てとバッキングストア](#allocation-and-backing-store)
* [非同期 i/o 要求を受信するためのクライアントドライバーの通知ルーチン](#client-drivers-notification-routine-for-receive-asynchronous-io-requests)
* [事前通知ケースでの非同期受信](#asynchronous-receive-in-the-pre-notification-case)

## <a name="allocated-addresses"></a>割り当てられたアドレス

バスドライバーでは、アドレス範囲を割り当てるための2つの異なる方法がサポートされています。 ドライバーが、ハードコーディングされたアドレスから始まる特定の範囲のアドレスを必要とする場合、要求の IRB の**Required1394Offset**メンバーのハードコーディングされたアドレスと、u のアドレス範囲の長さを指定できます。 **AllocateAddressRange. n 長さ**。 バスドライバーでは、2つの異なるドライバーが同じアドレスを2回割り当てることができます。 同じドライバーが同じアドレスで始まるアドレス範囲を2回割り当てようとした場合、バスドライバーはステータス\_コードが "成功" になっている要求を返しますが、要求自体は無視されます。

それ以外の場合、ドライバーは、バスドライバーが割り当てられたアドレスを選択できるようにします。 バスドライバーは、ドライバーによって割り当てられたすべてのアドレス範囲を追跡し、以前に未割り当てのアドレスのみを返します。

バスドライバーでは、アドレスが連続して割り当てられません。 アドレスは、バッキングストアとして提供される MDL に従ってセグメント化されます。 MDL 内の各セグメントは、アドレス範囲内の1つのセグメントに対応します。 割り当てられたアドレスが連続している必要があるドライバーは、非ページプールから連続するメモリを割り当てることができます。

ドライバーが、すべてのセグメントが特定のサイズよりも小さいことを保証する必要がある場合は、 **MaxSegmentSize**でそのサイズを指定できます。 セグメントの最大サイズを指定する必要がないドライバーは、 **MaxSegmentSize**を0に設定します。

バスドライバーは、IRB の**p1394AddressRange**メンバーによって指されているメモリ位置のアドレス範囲を返します。 デバイスドライバーは、最悪の場合のセグメント化シナリオでも、各アドレス\_範囲構造を保持するのに十分な大きさの配列を割り当てる必要があります。 ドライバーでセグメントサイズが指定されていない場合、またはセグメントの最大サイズがページ\_サイズよりも大きい場合、ドライバーは、アドレス\_と\_サイズ\_を使用して\_\_PAGES マクロをすることにより、最悪のケースを特定できます。バッキングストアに使用されるバッファー。 最大セグメントサイズがページ\_サイズよりも小さい場合、ドライバーはサイズが**u. AllocateAddressRange. nLength**/**u. Allocateaddressrange** + 2 の配列を割り当てる必要があります。

バスドライバーは、割り当てられたアドレスを返すと、 **u. AllocateAddressRange. haddressrange**に割り当てられた実際のアドレス範囲の数を記録します。

## <a name="allocation-and-backing-store"></a>割り当てとバッキングストア

バスドライバーは、ドライバーに代わって、すべての非同期パケット要求を受信します。 ドライバーの behest では、要求を透過的に処理したり、ドライバーに要求をディスパッチしたりできます。 アドレスの割り当て時にオプションを設定することにより、ドライバーはバスドライバーが各要求を処理する方法を選択できます。

1. ドライバーはアドレス範囲のバッキングストアを提供し、バスドライバーはバッキングストアを使用して、すべての読み取り、書き込み、ロック要求を透過的に処理します。

    ドライバーは、アドレスを割り当てるときに、バッキングストアとして機能するために、 **u. AllocateAddressRange**に mdl を提供できます。 バスドライバーは、ドライバーに対して割り当てられたアドレスの範囲に MDL をマップし、MDL から読み取りまたは書き込みを行うことによってすべての要求を処理します。 ホストコントローラーがサポートしている場合、トランザクションはホストコントローラーの DMA ハードウェアによって完全に処理されます。 可能な場合は、デバイスドライバーが、割り当てられたアドレスの範囲を選択できるようにする必要があります。バスドライバーは、各トランザクションの自動 DMA をサポートする1394のアドレスを選択します。

    ドライバーでは、[通知\_\_フラグを指定する必要があります。] には [**いいえ]** を指定します。

    以下に例を示します。

    ```cpp
    pIRB->u.AllocateAddressRange.Mdl = an MDL previously allocated by the driver.
    pIRB->u.AllocateAddressRange.fulNotificationOptions = NOTIFY_FLAGS_NEVER
    ```

    このオプションだけでは、ドライバーは、発生した IRQL でアドレス範囲を割り当てることもできます。 ドライバーは、ポートドライバーの物理的なマッピングルーチンを呼び出すことによって、通常の IRP 方式の通信をバイパスして、要求を直接ポートドライバーに送信できます。 デバイスドライバーは、ポートドライバーの物理的なマッピングルーチンに IRB を渡します。 その後、ポートドライバーはアドレス範囲を非同期的に割り当てます。ポートドライバーが完了すると、デバイスドライバーの通知ルーチンが呼び出され、 **u. allocateaddressrange. Callback**に渡され、パラメーターとして**u. Allocateaddressrange. Context**が渡されます。 通知ルーチンは、ディスパッチ\_レベルで呼び出されます。

    デバイスドライバーは、GET\_LOCAL\_HOST\_INFO 要求をバスドライバーに送信することによって、ポートドライバーの物理マッピングルーチンへのポインターを取得できます。これには、 **Nlevel** = GET\_PHYS\_ADDR\_ルーチンを使用します。 バスドライバーは GET\_ローカル\_ホスト\_INFO4 構造体を返します。これには、物理マッピングルーチンが含まれています。また、デバイスドライバーが IRB と共に物理マッピングルーチンに渡すコンテキストパラメーターも返されます。

    ドライバーが物理マッピングルーチンの要求を設定する方法の例を次に示します。 物理マッピングルーチンは変更されないため、ドライバーは通常、この要求を1回だけ送信します。

    ```cpp
    GET_LOCAL_HOST_INFO5 PhysMapInfo;
    pGetInfoIRB->FunctionNumber = GET_LOCAL_HOST_INFO;
    pGetInfoIRB->GET_PHYS_ADDR_ROUTINE;

    /* Driver submits the request. */
    ```

    この例を続行すると、ドライバーが物理マッピングルーチンを使用して昇格された IRQL で要求を送信する方法がわかります。

    ```cpp
    VOID AllocationCompletionRoutine(PVOID Context);
    /* Driver fills out the members of the IRB, including these: */
    pIRB->u.AllocateAddressRange.Mdl = an MDL previously allocated by the driver.
    pIRB->u.AllocateAddressRange.fulNotificationOptions = NOTIFY_FLAGS_NEVER
    pIRB->Callback = AllocationCompletionRoutine;
    pIRB->Context = information specific to this allocation the driver wants passed to its callback.

    /* Driver submits the request to the physical mapping routine. */
    PhysMapInfo.PhysAddrMappingRoutine(PhysMapInfo.Context, pIRB);

    /*
    The bus driver does the allocation asynchronously. When it's done, it will signal the driver by executing AllocationCompletionRoutine(pIRB->u.AllocateAddressRange.Context);
    */
    ```

2. ドライバーは、アドレス範囲のバッキングストアを提供します。 バスドライバーは、各 i/o トランザクションの完了後にドライバーに通知します。

    ドライバーは、1つの MDL または MDLs のリンクされたリストをバッキングストアとして提供できます。 ドライバーが1つの MDL を提供する場合、バスドライバーは非同期要求に応答して、MDL にデータをポンプします。 トランザクションが完了すると、ドライバーによって提供される通知コールバックを呼び出して、デバイスドライバーに通知します。

    デバイスドライバーは、IRB の**u. AllocateAddressRange. Callback**メンバーに通知ルーチンを提供します。 ドライバーは、\_XXX フラグの後\_通知\_フラグの少なくとも1つを設定する必要があります。 バスドライバーは、ルーチンを呼び出すと、通知\_情報構造を渡します。これは、mdl バッキングストア ( **mdl**内)、トランザクションが開始された mdl 内のバイトオフセット ( **uloffset**内)、および範囲の長さ (バイト単位) を指定します。影響を受けたアドレスの ( **Nlength**)。 通知ルーチンは、ディスパッチ\_レベルで呼び出されます。 ドライバーが**u. AllocateAddressRange**に渡すこの要求のコンテキスト情報。コンテキストは、通知\_情報の**コンテキスト**メンバーのバスドライバーによって渡されます。

    1つの MDL のみを使用すると、同期の問題が発生する可能性があります。デバイスは、ドライバーが読み取ることができるよりも速くアドレス範囲に書き込むことができます。 このような競合を回避するために、デバイスに書き込みアクセスのみがあるアドレスの場合、ドライバーは MDLs のリンクリストを指定できます。 **FifoSListHead**には、u **. Allocateaddressrange. fi%** スピンロックが含まれます。 バスドライバーは、各非同期要求パケットを受信すると、スピンロックを保持し、要求を満たすためにリストの最初の要素をポップします。 次に、ドライバーの通知ルーチンを呼び出します。

    NOTIFICATION\_INFO 構造体では、バスドライバーは、トランザクション ( **mdl**) を処理するために使用する mdl、影響を受ける最初のアドレスのバイトオフセット ( **uloffset**内)、影響を受けるアドレス範囲の長さ ( **nLength**)。 また、MDL ( **fifo**) の\_FIFO のアドレスも提供します。 ドライバーが通知ルーチンから戻る前に、 **Fifo**を使用してリストに要素を戻すか、同じサイズの別の MDL を提供する必要があります。それ以外の場合、バスドライバーは、デバイスからの書き込み要求を処理するために使用する MDLs から実行されます。

    この種類の通知を使用する拡張された例を次に示します。 グローバルに、ドライバーは、インタロック、シングルリンクリスト、およびスピンロックを作成します。 ドライバーは、リンクされたリストにアクセスする必要があり、IRQLs のスピンロックが発生したため、ページングされていないメモリ内にある必要があります。 通常、ドライバーはデバイスの拡張機能を保持します。

    ```cpp
    PSLIST_HEADER FifoSListHead;
    KSPIN_LOCK FifoSpinLock;

    ExInitializeSListHead(FifoSListHead);
    KeInitializeSpinLock(FifoSpinLock);
    ```

    ドライバーは、要求を送信するときに、関連する IRB メンバーを次のように設定できます。

    ```cpp
    VOID DriverNotificationRoutine(PNOTIFICATION_INFO NotificationInfo);

    pIRB->u.AllocateAddressRange.Mdl = NULL;
    pIRB->u.AllocateAddressRange.fulAccessType = ACCESS_FLAGS_READ;
    pIRB->u.AllocateAddressRange.fulNotificationOptions = NOTIFY_FLAGS_AFTER_WRITE;
    pIRB->u.AllocateAddressRange.FifoSListHead = FifoSListHead;
    pIRB->u.AllocateAddressRange.FifoSpinLock = FifoSpinLock;
    pIRB->u.AllocateAddressRange.Callback = DriverNotificationRoutine;
    pIRB->u.AllocateAddressRange.Context = context information specific to this request -- the bus driver will pass this as the Context member of the NOTIFICATION_INFO it passes to NotificationRoutine.
    ```

    コールバックでは、ドライバーは新しい MDL を割り当ててリストにプッシュするか、元の MDL をリストにプッシュする必要があります。 後者の場合、バスドライバーは、現在の MDL の元のアドレス\_FIFO に渡します。 現在の MDL を一覧にプッシュするドライバーの例を次に示します。

    ```cpp
    ExInterlockedPushEntrySList(FifoSListHead, NotificationInfo->Fifo->FifoList, FifoSpinLock);
    ```

    ドライバーで1つの MDL が元の割り当て要求のバッキングストアとして指定されている場合、ドライバーは1つ以上のアドレス範囲を返すことがあります。

3. バスドライバーは、要求が到着するたびにドライバーに信号を送り、パケットをドライバーに渡します。

    ドライバーは、IRB の**u. AllocateAddressRange. callback**メンバーにコールバックを提供します。 \_XXX フラグが無視された後\_通知\_フラグが無視され、すべてのパケットがドライバーに渡されて処理されます。

    ドライバーは、 **u. AllocateAddressRange**の**Mdl**、 **FifoSListHead**、および**fiの**メンバーを**NULL**に設定する必要があります。 次に、3種類すべての非同期要求パケットを受信したときに通知を受け取るドライバーの設定例を示します。

    ```cpp
    VOID DriverNotificationRoutine( IN PNOTIFICATION_INFO NotificationInfo );

    pIRB->u.AllocateAddressRange.Callback = DriverNotificationRoutine;
    pIRB->u.AllocateAddressRange.Context = information specific to this address range.
    pIRB->u.AllocateAddressRange.Mdl = NULL;
    pIRB->u.AllocateAddressRange.FifoSListHead = NULL;
    pIRB->u.AllocateAddressRange.FifoSpinLock = NULL;
    ```

    バスドライバーは、1つの連続した範囲のアドレスを割り当てます。

    バスドライバーは、ドライバーのコールバックルーチンに通知\_情報構造体を渡します。 デバイスドライバーは独自の応答パケットを作成する必要があります (詳細については、「IEEE 1394 の仕様」を参照してください)。独自のバッファーを割り当てて、作成した応答パケットを格納する必要があります。 応答パケットは、非ページプールまたはプローブおよびロックされているバッファーからのものである必要があります。

    通知\_情報内では、バスドライバーは、初期化されていない MDL を、**このメンバーに**提供します。 また、デバイスドライバーが応答パケットへのポインター ( **responsepacket**) と応答パケットの長さ ( **ResponseLength**) を入力することを想定しているメモリの場所へのポインターも提供します。 ドライバーは、カーネルイベントオブジェクトを提供することもできます。 バスドライバーは、トランザクションが完了すると、カーネルイベントオブジェクトに通知します。

    デバイスドライバーが通知ルーチンで必要な情報を入力する方法の例を次に示します。

    ```cpp
    /* Suppose the driver creates its response packet in PVOID ResponsePacket, of length ResponseLength. It has created a kernel event ResponseEvent. */
    MmInitializeMdl(NotificationInfo->ResponseMdl, ResponsePacket, ResponseLength);
    MmBuildMdlFForNonPagedPool(Notification->ResponseMdl);
    *(NotificationInfo->ResponsePacket) = ResponsePacket.
    *(NotificationInfo->ResponseLength) = ResponseLength;
    *(NotificationInfo)->ResponseEvent = Event;
    ```

## <a name="client-drivers-notification-routine-for-receive-asynchronous-io-requests"></a>非同期 i/o 要求を受信するためのクライアントドライバーの通知ルーチン

クライアントドライバーは、ドライバーの非同期受信通知ルーチンで次のタスクを実行する必要があります。

* クライアントドライバーに渡される[**NOTIFICATION\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_notification_info_w2k)構造体のメンバーを確認します。
* 読み取り/ロック要求が成功した場合 (応答パケットを介してデータを返す場合)、クライアントドライバーは次のことを行う必要があります。
  * 応答パケットデータに対して[**Wdfmemorycreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreate) (WDM ベースのクライアントドライバー用の[**exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag) ) を呼び出してメモリを割り当てます。
  * バッファーに、返されるデータを入力します。
  * の場合**は、このメンバーを**初期化し、バッファーを参照します。 [**MmInitializeMdl**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)と[**MmBuildMdlForNonPagedPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool)を呼び出すことができます。
  * **\*NotificationInfo-&gt;ResponsePacket**を設定してバッファーをポイントします。
  * **\*NotificationInfo-&gt;ResponseLength**を、返される応答データのサイズ (quadlet 読み取り要求の場合は 4) に設定します。
  * 応答イベントに対して[**Wdfmemorycreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreate) (WDM ベースのクライアントドライバー用の[**exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag) ) を呼び出してメモリを割り当てます。
  * イベントバッファーを指すように **\*NotificationInfo-&gt;ResponseEvent**を設定します。
  * イベントを待機するように作業項目をスケジュールし、応答イベントがシグナル状態になった後に応答パケットとイベントデータバッファーを解放します。
  * **Notificationinfo-&gt;** \_応答\_完了に設定します。

## <a name="asynchronous-receive-in-the-pre-notification-case"></a>事前通知ケースでの非同期受信

レガシ1394バスドライバーは、事前通知メカニズムを使用して非同期の受信トランザクションを完了できません。 詳細については、「[サポート技術情報: IEEE 1394 非同期受信応答が事前通知を使用して送信されない (2635883)](https://support.microsoft.com/help/2635883/ieee-1394-async-receive-response-not-sent-using-pre-notification)」を参照してください。

新しい1394バスドライバーでは、通知前のケースでのクライアントドライバーの通知コールバックルーチンの予期される動作は次のとおりです。

* [**Notification\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_notification_info_w2k)構造体の**Mdl**および**Fifo**メンバーが NULL の場合、事前通知が実行されます。
* [**NOTIFICATION\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_notification_info_w2k)構造体の**responsesemdl**、 **responsepacket**、 **RESPONSELENGTH**、および**responsepacket**メンバーを NULL にすることはできません。
* [**Notification\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_notification_info_w2k)構造体のテーブル間**notificationoptions**メンバーは、通知をトリガーしたアクション (読み取り、書き込み、ロック) を示す必要があります。 通知ルーチンが呼び出されるたびに、1つのフラグ (\_の読み取り後に\_通知\_フラグ、\_の書き込み後に\_フラグ\_に通知する、または\_ロックの後に\_フラグを通知する) のみを設定できます。
* 要求の種類を特定するには、ASYNC\_パケット構造の**Requestpacket-&gt;AP\_tCode**メンバーを調べます。 メンバーは、ブロックまたは quadlet の読み取り/書き込み、ロック要求の種類などの要求の種類を指定する TCODE を示します。 ASYNC\_パケット構造は、1394で宣言されています。
* [**NOTIFICATION\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_notification_info_w2k)の**Responsepacket**メンバーと**responsepacket**メンバーには、ポインターへのポインターが含まれています。 そのため、応答パケットと応答イベントへのポインターを適切に参照する必要があります。
* [**NOTIFICATION\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_notification_info_w2k)の**ResponseLength**メンバーは、ULONG 変数へのポインターです。 そのため、読み取り & ロック要求などの要求の応答データの長さを設定するときは、メンバーを適切に逆参照する必要があります。
* 1394クライアントドライバーは、応答パケットおよび応答イベント (非ページプールからの) にメモリを割り当て、応答が配信された後にそのメモリを解放する役割を担います。 作業項目をキューに配置し、作業項目が応答イベントを待機するようにすることをお勧めします。 このイベントは、応答が配信された後に1394バスドライバーによって通知されます。 その後、クライアントドライバーは、作業項目内のメモリを解放できます。
* [**NOTIFICATION\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_notification_info_w2k)構造体の値**には、** RCODE で定義されているいずれかの値を設定する必要があります。 応答\_が\_RCODE 以外の値に**設定されている場合は**、1394バスドライバーによってエラー応答パケットが送信されます。 読み取り要求またはロック要求の場合、要求はデータを返しません。 Windows 7 では、はメモリをリークする可能性があります。詳細については、「[サポート技術情報: IEEE 1394 バス2023232ドライバーのメモリリーク](https://support.microsoft.com/help/2023232)」を参照してください。
* 読み取り要求とロック要求の場合、[**通知\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_notification_info_w2k)構造の**responsepacket**メンバーは、非同期応答パケットで返されるデータをポイントする必要があります。

次のコード例は、作業項目の実装とクライアントドライバーの通知ルーチンを示しています。

```cpp
VOID
kmdf1394_NotifyRoutineWorkItem (
                                 IN WDFWORKITEM  WorkItem)
{
    NTSTATUS                 ntStatus;
    PNOTIFY_WORKITEM_CONTEXT notifyContext = GetNotifyWorkitemContext(WorkItem);

    Enter();

    ASSERT(notifyContext);

    ntStatus = KeWaitForSingleObject(
                                     &notifyContext->responseEvent,
                                     Executive,
                                     KernelMode,
                                     FALSE,
                                     NULL);
    if (!NT_SUCCESS(ntStatus))
    {
        DoTraceLevelMessage(TRACE_LEVEL_ERROR,
                            TRACE_FLAG_ASYNC,
                            "Wait on notify response event failed: %!STATUS!\n",
                            ntStatus);
    }

    WdfObjectDelete (WorkItem);

    Exit();
}

VOID
kmdf1394_NotificationCallback (
    IN PNOTIFICATION_INFO   NotifyInfo)
{
    PASYNC_PACKET           asyncPacket = (PASYNC_PACKET)NotifyInfo->RequestPacket;
    PASYNC_ADDRESS_DATA     asyncAddressData = NotifyInfo->Context;
    PULONG                  responseQuadlet;
    WDF_WORKITEM_CONFIG     workItemConfig;
    WDFWORKITEM             workItem;
    WDF_OBJECT_ATTRIBUTES   attributes;
    PNOTIFY_WORKITEM_CONTEXT notifyContext;
    NTSTATUS                ntStatus;

    Enter();

    DoTraceLevelMessage(TRACE_LEVEL_INFORMATION,
                        TRACE_FLAG_ASYNC,
                        "NotifyInfo Mdl %p ulOffset %08x nLength %08x fulNotificationOptions %08x Context %p RCode %x Pkt %p\n",
                        NotifyInfo->Mdl,
                        NotifyInfo->ulOffset,
                        NotifyInfo->nLength,
                        NotifyInfo->fulNotificationOptions,
                        NotifyInfo->Context,
                        NotifyInfo->ResponseCode,
                        asyncPacket);

    if (NotifyInfo->Mdl)
    {
        // Post-Notification
        switch (NotifyInfo->fulNotificationOptions)
        {
            case NOTIFY_FLAGS_AFTER_LOCK:
                NotifyInfo->ResponseCode = RCODE_TYPE_ERROR;
                break;

            case NOTIFY_FLAGS_AFTER_WRITE:
                NotifyInfo->ResponseCode = RCODE_TYPE_ERROR;
                break;

            case NOTIFY_FLAGS_AFTER_READ:
                // Don't touch ResponseCode if no error
                // NotifyInfo->ResponseCode = RCODE_RESPONSE_COMPLETE;
                break;

            default:
                NotifyInfo->ResponseCode = RCODE_TYPE_ERROR;
                break;
        }
    }
    else
    {
        // Pre-Notification
        if (asyncPacket)
        {
            if ( !NotifyInfo->ResponseMdl ||
                    !NotifyInfo->ResponsePacket ||
                    !NotifyInfo->ResponseLength ||
                    !NotifyInfo->ResponseEvent )
            {
                DoTraceLevelMessage(TRACE_LEVEL_ERROR,
                                    TRACE_FLAG_ASYNC,
                                    "Pre-Notification failure: missing Response field(s)!\n");
                DoTraceLevelMessage(TRACE_LEVEL_ERROR,
                                    TRACE_FLAG_ASYNC,
                                    "ResponseMdl %p\tResponsePacket %p\tResponseLength %p\tResponseEvent %p\n",
                                    NotifyInfo->ResponseMdl, NotifyInfo->ResponsePacket,
                                    NotifyInfo->ResponseLength, NotifyInfo->ResponseEvent);
                if (NotifyInfo->ResponsePacket != NULL)
                {
                    DoTraceLevelMessage(TRACE_LEVEL_ERROR,
                                        TRACE_FLAG_ASYNC,
                                        "\t*ResponsePacket %p\n",
                                        *NotifyInfo->ResponsePacket);
                }
                NotifyInfo->ResponseCode = RCODE_TYPE_ERROR;
            }
            else if ( NULL == asyncAddressData )
            {
                DoTraceLevelMessage(TRACE_LEVEL_ERROR,
                                    TRACE_FLAG_ASYNC,
                                    "Pre-Notification failure: missing Notify Context!\n");
                NotifyInfo->ResponseCode = RCODE_TYPE_ERROR;
            }
            else
            {
                DoTraceLevelMessage(TRACE_LEVEL_INFORMATION,
                                    TRACE_FLAG_ASYNC,
                                    "AddrData %p DevExt %p Buffer %p Len %x hAddrRange %!HANDLE! Mdl %p\n",
                                    asyncAddressData,
                                    asyncAddressData->DeviceExtension,
                                    asyncAddressData->Buffer,
                                    asyncAddressData->nLength,
                                    asyncAddressData->hAddressRange,
                                    asyncAddressData->pMdl);

                switch (asyncPacket->AP_tCode)
                {
                    case TCODE_LOCK_REQUEST:
                        NotifyInfo->ResponseCode = RCODE_TYPE_ERROR;
                        break;

                    case TCODE_WRITE_REQUEST_QUADLET:
                    case TCODE_WRITE_REQUEST_BLOCK:
                        NotifyInfo->ResponseCode = RCODE_TYPE_ERROR;
                        break;

                    case TCODE_READ_REQUEST_BLOCK:
                        NotifyInfo->ResponseCode = RCODE_DATA_ERROR;
                        break;

                    case TCODE_READ_REQUEST_QUADLET:
                        // only implementing Quadlet Read for now

                        // Create a WdfWorkItem, with notifyResponse as its context,
                        // to handle waiting for the Response Event & cleaning up all the response stuff

                        WDF_WORKITEM_CONFIG_INIT (&workItemConfig, kmdf1394_NotifyRoutineWorkItem);

                        WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&attributes, NOTIFY_WORKITEM_CONTEXT);

                        attributes.ParentObject = WdfObjectContextGetObject(asyncAddressData->DeviceExtension);

                        ntStatus = WdfWorkItemCreate( &workItemConfig,
                            &attributes,
                            &workItem);

                        if (!NT_SUCCESS (ntStatus))
                        {
                            DoTraceLevelMessage(TRACE_LEVEL_ERROR,
                                                TRACE_FLAG_ASYNC,
                                                "Failed to create workitem %x\n",
                                                ntStatus);

                            NotifyInfo->ResponseCode = RCODE_DATA_ERROR;
                            break;
                        }

                        notifyContext = GetNotifyWorkitemContext(workItem);

                        notifyContext->asyncAddressData = asyncAddressData;

                        // NotifyInfo->ResponsePacket
                        // memory location that the driver fills in with
                        // a pointer to the beginning of its response packet

                        // parent this memory object to the workitem so both can be cleaned up together
                        WDF_OBJECT_ATTRIBUTES_INIT (&attributes);
                        attributes.ParentObject = workItem;

                        ntStatus = WdfMemoryCreate(
                                                   &attributes,
                                                   NonPagedPool,
                                                   POOLTAG_KMDF_VDEV,
                                                   sizeof(ULONG),
                                                   &notifyContext->responseMemory,
                                                   &responseQuadlet);

                        if (!NT_SUCCESS(ntStatus) || !responseQuadlet)
                        {
                            DoTraceLevelMessage(TRACE_LEVEL_ERROR,
                                                TRACE_FLAG_ASYNC,
                                                "Failed to allocate Response Data Memory: %!STATUS!\n",
                                                ntStatus);

                            WdfObjectDelete (workItem);

                            NotifyInfo->ResponseCode = RCODE_DATA_ERROR;
                            break;
                        }

                        RtlFillMemory(responseQuadlet, sizeof(ULONG), 0x8F);    // dummy data for testing

                        // NotifyInfo->ResponseMdl
                        // initialize MDL for a nonpageable buffer,
                        // and fill the buffer with the response packet
                        MmInitializeMdl(NotifyInfo->ResponseMdl,
                                        responseQuadlet,
                                        sizeof(ULONG));
                        MmBuildMdlForNonPagedPool(NotifyInfo->ResponseMdl);

                        // do what it looks like the New (KMDF) stack expects,
                        // which is that NotifyInfo->ResponsePacket points to the
                        // data following the Async Packet header
                        *NotifyInfo->ResponsePacket = (PVOID)&responseQuadlet;

                        // NotifyInfo->ResponseEvent
                        // memory location that the driver fills in with
                        // the kernel event the bus driver should use to signal
                        // that it has completed sending the response packet
                        KeInitializeEvent(&notifyContext->responseEvent, NotificationEvent, FALSE);

                        *NotifyInfo->ResponseEvent = &notifyContext->responseEvent;

                        // NotifyInfo->ResponseLength
                        // memory location that the driver fills in with
                        // the length of its response packet
                        *NotifyInfo->ResponseLength = sizeof(ULONG);

                        // NotifyInfo->ResponseCode
                        // specifies the result of the driver's response to the request
                        NotifyInfo->ResponseCode = RCODE_RESPONSE_COMPLETE;

                        // Enqueue the work item to clean up after notification completion
                        WdfWorkItemEnqueue (workItem);

                        DoTraceLevelMessage(TRACE_LEVEL_INFORMATION,
                                            TRACE_FLAG_ASYNC,
                                            "Pre-Notification: Read Quadlet: Notify Response Handle %!HANDLE! Data %08x Event %p\n",
                                            notifyContext->responseMemory,
                                            *responseQuadlet,
                                            &notifyContext->responseEvent);

                        break;

                    default:
                        NotifyInfo->ResponseCode = RCODE_TYPE_ERROR;
                        break;
                } // switch (asyncPacket->AP_tCode)
            } // else [pre-notification params OK]
        } // if (asyncPacket)
        else
        {
            DoTraceLevelMessage(TRACE_LEVEL_ERROR,
                                TRACE_FLAG_ASYNC,
                                "Pre-Notification failure: no RequestPacket!\n");
            NotifyInfo->ResponseCode = RCODE_DATA_ERROR;
        }
    }

    ExitS( NotifyInfo->ResponseCode | RCODE_STATUS_MASK );
    return;
} // kmdf1394_NotificationCallback
```
