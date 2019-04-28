---
title: IEEE 1394 バスでの非同期 I/O 要求パケットの受信
description: コンピューター自体は、IEEE 1394 バス上のノードし、非同期 I/O 要求を受信できます。
ms.assetid: 7b8eaf40-7fdc-4c25-86a7-8377d2d51877
keywords:
- 非同期 I/O 要求の受信
- アドレス範囲の割り当てください。
- WDK の IEEE 1394 をアドレスします。
- WDK の IEEE 1394 のバッキング ストア
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 695ba4688e41c73a1d2b21d3652912a3b9e7f8c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370980"
---
# <a name="receiving-asynchronous-io-request-packets-on-the-ieee-1394-bus"></a>IEEE 1394 バスでの非同期 I/O 要求パケットの受信

コンピューター自体は、IEEE 1394 バス上のノードし、非同期 I/O 要求を受信できます。 ドライバーがコンピューターの IEEE 1394 のアドレス空間のアドレスの範囲を割り当てるし、要求を送信することで、外部のノードから要求を受信\_ALLOCATE\_アドレス\_バス ドライバーに範囲の要求。

ドライバーが、アドレスの範囲を割り当てるとき、ことができますトランザクションの種類、デバイス可能性があります送信指定割り当て済みのアドレスを 1 つ以上のアクセスを指定することで\_フラグ\_型\_読み取り、アクセス\_フラグ\_型\_書き込み、またはアクセス\_フラグ\_型\_内のロック、 **u.AllocateAddressRange.fulAccessType**要求の IRB のメンバー。 要求が自動的に、指定した型のいずれかが失敗します。

2 つの異なるドライバーでは、同じアドレス範囲を割り当てることもできます。 既定では、バス ドライバーは、要求を自動的に demultiplexes し、ドライバー、ドライバーのデバイスに由来する割り当て済みアドレスで要求のみが表示されます。 ドライバーは、アクセスを指定することで、バス上のすべてのノードで、アドレスに送信するすべてのパケットを受信したことを要求できます\_フラグ\_型\_でフラグをブロードキャスト**u.AllocateAddressRange.fulAccessType**.

* [割り当て済みアドレス](#allocated-addresses)
* [割り当てとバッキング ストア](#allocation-and-backing-store)
* [クライアント ドライバーの通知ルーチンが非同期 I/O 要求を受信します。](#client-drivers-notification-routine-for-receive-asynchronous-io-requests)
* [非同期の受信の場合は事前の通知](#asynchronous-receive-in-the-pre-notification-case)

## <a name="allocated-addresses"></a>割り当て済みアドレス

バス ドライバーでは、アドレス範囲を割り当てることの 2 つの異なる戦略をサポートします。 ハード コーディングされたアドレスを指定できます、ドライバーは、ハード コーディングされたアドレスで始まるアドレスの特定の範囲を必要とする場合、 **u.AllocateAddressRange.Required1394Offset**要求の IRB との長さのメンバー、アドレス範囲で**u.AllocateAddressRange.nLength**します。 バス ドライバーにより、2 回、同じアドレスを割り当てることの 2 つの異なるドライバー。 同じドライバーが、アドレスで始まる範囲と同じアドレス 2 回の割り当てを試みると、バス ドライバーは、要求の状態の状態コードを返します\_が成功した場合、要求自体は無視されます。

それ以外の場合、ドライバーは、割り当て済みのアドレスを選択するバス ドライバーを許可できます。 バス ドライバーはドライバーによって割り当てられたすべてのアドレス範囲の追跡し、は以前に割り当てられていないアドレスのみを返します。

バス ドライバーが、アドレスを連続して割り当てられません。 アドレスは、バッキング ストアとして提供される MDL に従って分割されます。 MDL 内の各セグメントは、アドレス範囲内の 1 つのセグメントに対応します。 連続して割り当て済みアドレスが必要なドライバーは、非ページ プールからの連続したメモリを割り当てることができます。

そのサイズを指定できますが、すべてのセグメントが、特定のサイズよりも小さいことを保証するために、ドライバーが必要な場合**u.AllocateAddressRange.MaxSegmentSize**します。 セットのサイズを最大セグメントを指定する必要のないドライバー **u.AllocateAddressRange.MaxSegmentSize**をゼロにします。

バス ドライバーによって示されるメモリ位置のアドレス範囲を返します、 **u.AllocateAddressRange.p1394AddressRange** IRB のメンバー。 デバイス ドライバーは、各アドレスを保持するために十分な大きさである配列を割り当てる必要があります\_最悪のケースのセグメント化のシナリオであっても、範囲の構造体。 ドライバーはセグメントのサイズを指定していないか、そのセグメントの最大サイズがページよりも大きい場合\_サイズ、ドライバーは、アドレスを使用して、最悪の場合を決定することができますし、\_AND\_サイズ\_TO\_スパン\_バッキング ストアに使用されるバッファーにページ マクロです。 セグメントの最大サイズがページよりも小さい場合\_サイズ、ドライバーはサイズの配列を割り当てる必要があります**u.AllocateAddressRange.nLength**/**u.AllocateAddressRange.MaxSegmentSize** + 2。

実際に割り当てられたアドレスの範囲の数を記録、バス ドライバーには、割り当て済みのアドレスが返される、ときに**u.AllocateAddressRange.hAddressRange**します。

## <a name="allocation-and-backing-store"></a>割り当てとバッキング ストア

バス ドライバーでは、ドライバーの代わりにすべてのパケットの非同期要求を受信します。 ドライバーの要請、要求を透過的に処理することができます。 またはドライバーに要求をディスパッチできます。 アドレスを割り当てるときのオプションを設定して、ドライバーは、バス ドライバーが各要求を処理する方法を選択できます。

1. ドライバーは、アドレスの範囲のバッキング ストアを提供し、バス ドライバーはすべての読み取り、書き込み、およびロックの要求を透過的に処理すると、バッキング ストアを使用しています。

    MDL を指定できます、ドライバーがアドレスを割り当てるときに**u.AllocateAddressRange.Mdl**バッキング ストアとして機能します。 バス ドライバーでは、ドライバーを割り当てるによって読み取りまたは書き込み MDL からすべての要求を処理するアドレスの範囲に MDL がマップされます。 ホスト コント ローラーがサポートする場合、トランザクションは、ホスト コント ローラーの DMA のハードウェアによって完全処理されます。 可能であれば、デバイス ドライバーが割り当てられたアドレスの範囲を選択するバス ドライバーを許可する必要があります。 バス ドライバーがトランザクションごとに自動 DMA をサポートする 1394 アドレスを選択します。

    ドライバーは、通知を指定する必要があります\_フラグ\_の NEVER **u.AllocateAddressRange.fulNotificationOptions**します。

    次に例を示します。

    ```cpp
    pIRB->u.AllocateAddressRange.Mdl = an MDL previously allocated by the driver.
    pIRB->u.AllocateAddressRange.fulNotificationOptions = NOTIFY_FLAGS_NEVER
    ```

    だけでこのオプションのドライバーも同時に、発生した IRQL のアドレス範囲を割り当てることができます。 ドライバーは、直接ポート ドライバー、ポート ドライバーの物理へのマッピングのルーチンを呼び出すことによって、通信の通常の IRP メソッドをバイパスする要求を送信できます。 デバイス ドライバーは、ポート ドライバーの物理へのマッピングのルーチンを IRB を渡します。 ポート ドライバーは、アドレスの範囲を非同期的に割り当てます、デバイス ドライバーの通知呼び出しポート ドライバーが完了したら、日常的な渡された**u.AllocateAddressRange.Callback**、し、渡します**u.AllocateAddressRange.Context**パラメーターとして。 通知のルーチンはディスパッチ時に呼び出されます\_レベル。

    デバイス ドライバーは GET を送信してポート ドライバーの物理へのマッピングのルーチンへのポインターを取得することができます\_ローカル\_ホスト\_で情報を要求、バス ドライバーに**nLevel** = GET\_物理サイズ\_ADDR\_ルーチン。 バス ドライバー返します GET\_ローカル\_ホスト\_情報 4 構造は、物理へのマッピングのルーチン、およびデバイス ドライバーが、IRB と共に物理マッピング ルーチンに渡されるコンテキスト パラメーターが含まれています。

    物理へのマッピングのルーチンの要求をドライバーをセットアップする方法の例を次に示します。 物理マッピング ルーチンが変更されない、ので、ドライバーは通常はこの要求を 1 回のみ送信します。

    ```cpp
    GET_LOCAL_HOST_INFO5 PhysMapInfo;
    pGetInfoIRB->FunctionNumber = GET_LOCAL_HOST_INFO;
    pGetInfoIRB->GET_PHYS_ADDR_ROUTINE;

    /* Driver submits the request. */
    ```

    ドライバーが物理へのマッピングのルーチンを使用して、管理者特権での IRQL で要求を送信する方法の例に続けて、示します。

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

2. ドライバーは、アドレス範囲のバッキング ストアを提供します。 I/O の各トランザクションが完了した後、バス ドライバーはドライバーを通知します。

    ドライバーでは、バッキング ストアとして、1 つの MDL または MDLs のリンク リストのいずれかを指定できます。 ドライバーは、1 つの MDL を提供する場合、バス ドライバーは、非同期の要求に応答 MDL の内外にデータをポンプです。 トランザクションが完了すると、ドライバーによって提供される通知コールバックを呼び出すことによって、デバイス ドライバーを通知します。

    デバイス ドライバーの通知ルーチンを提供する、 **u.AllocateAddressRange.Callback** IRB のメンバー。 ドライバーを設定する必要があります、通知の少なくとも 1 つ\_フラグ\_AFTER\_XXX フラグ。 ルーチンを呼び出す、バス ドライバーとときに、通知を渡します\_情報構造体 MDL のバッキング ストアを指定します (で**Mdl**)、トランザクションの開始位置 MDL 内のバイト オフセット (で**ulOffset**)、および影響を受けるアドレスの範囲の長さ (バイト単位) (で**されて**)。 通知のルーチンはディスパッチ時に呼び出されます\_レベル。 この要求で、ドライバーに合格するためのコンテキスト情報**u.AllocateAddressRange.Context**バス ドライバーに渡し、**コンテキスト**通知のメンバー\_情報。

    同期の問題のある程度のリスクがある 1 つだけ MDL を使用して、: デバイスがそこから読み取ることができます、ドライバーよりも高速のアドレス範囲に書き込むことがあります。 アドレスのデバイスのみにある、ドライバーの書き込みアクセスで MDLs のリンク リストを提供できます、このような競合を回避するために**u.AllocateAddressRange.FifoSListHead**、スピン ロックと**u です。AllocateAddressRange.FifoSpinLock**します。 バス ドライバーでは、各非同期要求パケットを受信するときに、スピン ロックを保持を要求を処理するリストの最初の要素をポップします。 これは、後、ドライバーの通知ルーチンを呼び出します。

    通知では、\_情報構造、バス ドライバーを提供します、トランザクションを処理するために使用する MDL (で**Mdl**)、影響を受けた最初のアドレスのバイト オフセット (で**ulOffset**)、および影響を受けるアドレスの範囲の長さ (で**されて**)。 アドレスも用意されています。\_MDL の FIFO (で**Fifo**)。 ドライバーがその通知ルーチンから戻る前に、使用するかを行ってください**Fifo** 、一覧に戻り、要素をプッシュまたは同じの別の MDL を提供するサイズである場合は、バス ドライバーが不足 MDLs 書き込みの処理に使用するには。デバイスからの要求。

    この通知の種類を使用する拡張例を次に示します。 グローバルに、ドライバーは、インタロックされた、シングル リンク リストと、スピン ロックを作成します。 ドライバーは、非ページ メモリにする必要があるため、リンク リストと、発生の Irql でスピン ロックにアクセスする必要があります。 通常、ドライバーに保管して、デバイスの拡張機能。

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

    コールバックでは、ドライバーを新しい MDL を割り当てると、一覧の上にそれをプッシュまたはプッシュ元 MDL のいずれかのニーズのバックアップ リスト。 後者の場合、バス ドライバーは、元のアドレスを渡す\_現在 MDL の FIFO です。 ドライバーの一覧に戻り、現在 MDL のプッシュの例を次に示します。

    ```cpp
    ExInterlockedPushEntrySList(FifoSListHead, NotificationInfo->Fifo->FifoList, FifoSpinLock);
    ```

    ドライバーは、元の割り当て要求にストアをバックアップとして 1 つの MDL を指定する場合、ドライバーは、1 つまたは複数のアドレス範囲を返す可能性があります。

3. バス ドライバーでは、毎回の要求が到着すると、およびドライバーにパケットを渡します、ドライバーを通知します。

    ドライバーでのコールバックを提供する、 **u.AllocateAddressRange.Callback** IRB のメンバー。 NOTIFY\_フラグ\_AFTER\_XXX フラグは無視され、すべてのパケットが処理するためにドライバーに渡されます。

    ドライバーを設定する必要があります、 **Mdl**、 **FifoSListHead**、および**FifoSpinLock**のメンバー **u.AllocateAddressRange**に**NULL**します。 次の 3 種類すべての非同期要求パケットを受信したときに通知されるドライバーの設定の例に示します。

    ```cpp
    VOID DriverNotificationRoutine( IN PNOTIFICATION_INFO NotificationInfo );

    pIRB->u.AllocateAddressRange.Callback = DriverNotificationRoutine;
    pIRB->u.AllocateAddressRange.Context = information specific to this address range.
    pIRB->u.AllocateAddressRange.Mdl = NULL;
    pIRB->u.AllocateAddressRange.FifoSListHead = NULL;
    pIRB->u.AllocateAddressRange.FifoSpinLock = NULL;
    ```

    バス ドライバーでは、単一の連続したアドレスの範囲を割り当てます。

    バス ドライバーに渡します通知\_ドライバーのコールバック ルーチンへの情報の構造体。 デバイス ドライバーは、独自の応答パケットを作成する必要があります (詳細については、IEEE 1394 の仕様を参照)、および作成応答パケットを格納するバッファーを割り当てる必要があります。 非ページ プールとプローブおよびロックされたバッファーから、応答パケットがある必要があります。

    通知内で\_については、バス ドライバーで初期化されていない MDL、 **ResponseMdl**メンバー。 想定される応答パケットへのポインターを入力するデバイス ドライバーのメモリ ロケーションへのポインターも用意されています (で**ResponsePacket**)、および応答パケットの長さ (で**ResponseLength**)。 ドライバーでは、カーネル イベント オブジェクトも提供できます。 トランザクションが完了すると、バス ドライバーは、カーネル イベント オブジェクトを通知します。

    その通知ルーチンで必要な情報でデバイス ドライバーの塗りつぶしできる方法の例を次に示します。

    ```cpp
    /* Suppose the driver creates its response packet in PVOID ResponsePacket, of length ResponseLength. It has created a kernel event ResponseEvent. */
    MmInitializeMdl(NotificationInfo->ResponseMdl, ResponsePacket, ResponseLength);
    MmBuildMdlFForNonPagedPool(Notification->ResponseMdl);
    *(NotificationInfo->ResponsePacket) = ResponsePacket.
    *(NotificationInfo->ResponseLength) = ResponseLength;
    *(NotificationInfo)->ResponseEvent = Event;
    ```

## <a name="client-drivers-notification-routine-for-receive-asynchronous-io-requests"></a>クライアント ドライバーの通知ルーチンが非同期 I/O 要求を受信します。

クライアント ドライバーは、次を実行する必要があります、ドライバーの内の非同期タスクの受信通知ルーチン。

* メンバーを確認する、 [**通知\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff537437)クライアント ドライバーに渡される構造体。
* (応答パケットからのデータを返す場所)、読み取り/ロックの成功した要求のクライアント ドライバーである必要があります。
  * 呼び出すことによってメモリを割り当てる[ **WdfMemoryCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff548706) ([**exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520) WDM ベースのクライアント ドライバー用) の応答パケット データ。
  * 返されるデータには、そのバッファーを入力します。
  * 初期化、 **ResponseMdl**メンバーと、バッファーの参照。 呼び出すことができます[ **MmInitializeMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff554568)と[ **MmBuildMdlForNonPagedPool**](https://msdn.microsoft.com/library/windows/hardware/ff554498)します。
  * 設定 **\*NotificationInfo -&gt;ResponsePacket**バッファーを指すようにします。
  * 設定 **\*NotificationInfo -&gt;ResponseLength** 、返される応答データのサイズには 4 の要求を読み取り、作成されます)。
  * 呼び出すことによってメモリを割り当てる[ **WdfMemoryCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff548706) ([**exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520) WDM ベースのクライアント ドライバー用) の応答イベントです。
  * 設定 **\*NotificationInfo -&gt;ResponseEvent**イベント バッファーを指すようにします。
  * イベントで待機する作業項目をスケジュールし、応答イベントが通知された後に、応答パケットとイベントのデータ バッファーを解放します。
  * 設定**NotificationInfo -&gt;ResponseCode** RCODE に\_応答\_完了します。

## <a name="asynchronous-receive-in-the-pre-notification-case"></a>非同期の受信の場合は事前の通知

非同期を完了する、従来の 1394 バス ドライバーは失敗では、事前通知メカニズムを使用してトランザクションを受信します。 詳細については、次を参照してください。[ナレッジ ベース。未送信の事前通知 (2635883) を使用して、IEEE 1394 非同期受信応答](http://support.microsoft.com/kb/2635883)します。

新しい 1394 バス ドライバーの場合は、事前の通知の場合は、クライアント ドライバーの通知コールバック ルーチンの想定される動作がとおりです。

* 場合**Mdl**と**Fifo**のメンバー、 [**通知\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff537437)構造体が null の場合、次の事前通知しています実行されます。
* **ResponseMdl**、 **ResponsePacket**、 **ResponseLength**、および**ResponseEvent**のメンバー、 [ **通知\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff537437)構造では、NULL は指定できません。
* **FulNotificationOptions**のメンバー、 [**通知\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff537437)構造がトリガーされたアクション (読み取り、書き込み、ロック) を示す必要があります、通知します。 1 つのみのフラグ (通知\_フラグ\_AFTER\_読み取り]、[通知\_フラグ\_AFTER\_書き込み、または通知\_フラグ\_AFTER\_ロック) を設定できます毎回、通知ルーチンが呼び出されます。
* 検査することによって、要求の種類を識別できます、 **RequestPacket -&gt;AP\_は**、非同期のメンバー\_パケットの構造体。 メンバーはブロックまたは作成されます読み取り/書き込み、ロック要求の種類など、要求の種類を指定することを示します。 ASYNC\_1394.h でパケットの構造体が宣言されています。
* **ResponsePacket**と**ResponseEvent**のメンバー [**通知\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff537437)ポインターへのポインターが含まれています。 したがって、応答パケットと応答イベントへのポインターを適切に参照する必要があります。
* **ResponseLength**のメンバー [**通知\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff537437) ULONG 変数へのポインターです。 そのため、する必要があります設定するときに要求の応答データの長さなどの読み取りのために、メンバーを適切に逆参照 & ロック要求)。
* 1394 クライアント ドライバーは、(非ページ プールの場合) から、応答パケットと応答イベントのメモリの割り当てと、応答が配信された後、そのメモリを解放します。 作業項目がキューに登録され、作業項目は、応答イベントで待機する必要がありますのことをお勧めします。 応答が配信された後、1394 バス ドライバーによって、そのイベントがシグナル状態します。 クライアント ドライバーは、作業項目内のメモリを解放し、できます。
* **ResponseCode**内のメンバー、 [**通知\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff537437) 1394.h で定義されている \FLAGS 値の 1 つの構造を設定する必要があります。 場合**ResponseCode** RCODE 以外の値に設定されている\_応答\_完了、1394 バス ドライバーは、エラー応答パケットを送信します。 読み取りまたはロックの要求の場合、要求では、すべてのデータは返されません。 Windows 7 では、メモリ リークが発生、詳細については「[ナレッジ ベース。IEEE 1394 のバス ドライバー (2023232) の非同期の通知コールバックの実行中のメモリ リーク](http://support.microsoft.com/kb/2023232)します。
* 読み取りとロックの要求に対して、 **ResponsePacket**のメンバー、 [**通知\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff537437)構造体で返されるデータを指す必要があります、非同期応答パケットです。

次のコード例では、作業項目の実装と、クライアント ドライバーの通知ルーチンを示します。

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
