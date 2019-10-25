---
title: 0x7C BUGCODE_NDIS_DRIVER のバグチェック
description: BUGCODE_NDIS_DRIVER のバグチェックの値は0x0000007C です。 このバグチェックは、オペレーティングシステムがネットワークドライバーでエラーを検出したことを示します。
ms.assetid: 0f2c2e9c-2889-4d99-b653-0ee1d4c2be0e
keywords:
- 0x7C BUGCODE_NDIS_DRIVER のバグチェック
- BUGCODE_NDIS_DRIVER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BUGCODE_NDIS_DRIVER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: efa1865aa49478a04f07fde618901c36a95a73b4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837991"
---
# <a name="bug-check-0x7c-bugcode_ndis_driver"></a>バグチェック 0x7C: コード\_NDIS\_ドライバーを修正します


バグコード\_NDIS\_ドライバーのバグチェックには、0x0000007C の値が含まれています。 このバグチェックは、オペレーティングシステムがネットワークドライバーでエラーを検出したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="bugcode_ndis_driver-parameters"></a>\_NDIS\_ドライバーパラメーターのバグコード


パラメーター1は違反の種類を示します。 他のパラメーターの意味は、パラメーター1の値によって異なります。 パラメーターの値が "0" の場合、これは使用されないことを意味します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />

</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター1</th>
<th align="left">パラメーター1の値とエラーの原因</th>
<th align="left">パラメータ 2</th>
<th align="left">パラメーター3</th>
<th align="left">パラメーター4</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>NDIS_BUGCHECK_ALLOCATE_SHARED_MEM_HIGH_IRQL</p>
<p>発生した IRQL で<strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocatesharedmemory" data-raw-source="[NdisMAllocateSharedMemory](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocatesharedmemory)">NdisMAllocateSharedMemory</a></strong>というドライバーが呼び出されました。</p></td>
<td align="left"><p>特定のミニポートアダプターブロックのアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd netadapter</a></strong>を実行してください。</p></td>
<td align="left"><p>要求された共有メモリの長さ</p></td>
<td align="left"><p>現在の IRQL</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>NDIS_BUGCHECK_SHARED_MEM_CORRUPTION</p>
<p><strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocatesharedmemory" data-raw-source="[NdisMAllocateSharedMemory](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocatesharedmemory)">NdisMAllocateSharedMemory</a></strong>の呼び出し中に、以前に割り当てられた共有メモリページが破損したことが NDIS によって検出されました。</p></td>
<td align="left"><p>特定のミニポートアダプターブロックのアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd netadapter</a></strong>を実行してください。</p></td>
<td align="left"><p>破損した共有メモリページ</p></td>
<td align="left"><p>ドライバーによる共有メモリの割り当てを追跡する NDIS_WRAPPER_CONTEXTE のアドレス</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03</p></td>
<td align="left"><p>NDIS_BUGCHECK_FREE_INVALID_SHARED_MEM</p>
<p>既に解放されている共有メモリアドレスを使用して、 <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreesharedmemory" data-raw-source="[NdisMFreeSharedMemory](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreesharedmemory)">NdisMFreeSharedMemory</a></strong> (<strong>Async</strong>) という名前のミニポートドライバー。</p></td>
<td align="left"><p>特定のミニポートアダプターブロックのアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd netadapter</a></strong>を実行してください。</p></td>
<td align="left"><p>この共有メモリが割り当てられたページ</p></td>
<td align="left"><p>共有メモリの仮想アドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x04</p></td>
<td align="left"><p>NDIS_BUGCHECK_UNLOAD_DRIVER_INVALID_PARAMETER</p>
<p><strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device" data-raw-source="[AddDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)">AddDevice</a></strong>が、NDIS に登録されているドライバーの一覧にないドライバーを使用して呼び出されました。</p>
<p>特別なインストルメント化された NDIS でのみ有効です。</p></td>
<td align="left"><p>NDIS_M_DRIVER_BLOCK のアドレス</p></td>
<td align="left"><p>DRIVER_OBJECT のアドレス</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x05</p></td>
<td align="left"><p>NDIS_BUGCHECK_RECVD_PACKET_IN_USE_BAD_STACK_LOCATION</p>
<p>イーサネットドライバーは、プロトコルスタックによって現在使用されていたパケット記述子を使用してパケットを受信したことを示していました。</p>
<p>スタックパケットの場所を確認することでキャッチされます。</p></td>
<td align="left"><p>特定のミニポートアダプターブロックのアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd netadapter</a></strong>を実行してください。</p></td>
<td align="left"><p>ドライバーによって使用されるパケット記述子のアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-pkt.md" data-raw-source="[!ndiskd.pkt](-ndiskd-pkt.md)">! ndiskd pkt</a></strong>を実行してください。</p></td>
<td align="left"><p>このパケット記述子を格納したパケット配列のアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x06</p></td>
<td align="left"><p>NDIS_BUGCHECK_RECVD_PACKET_IN_USE_BAD_REF_COUNT</p>
<p>イーサネットドライバーは、プロトコルスタックによって現在使用されていたパケット記述子を使用してパケットを受信したことを示していました。</p>
<p>パケット参照カウントを調べて、キャッチしました。</p></td>
<td align="left"><p>特定のミニポートアダプターブロックのアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd netadapter</a></strong>を実行してください。</p></td>
<td align="left"><p>ドライバーによって使用されるパケット記述子のアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-pkt.md" data-raw-source="[!ndiskd.pkt](-ndiskd-pkt.md)">! ndiskd pkt</a></strong>を実行してください。</p></td>
<td align="left"><p>このパケット記述子を格納したパケット配列のアドレス</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x07</p></td>
<td align="left"><p>FDDI ドライバーは、プロトコルスタックによって現在使用されていたパケット記述子を使用してパケットを受信したことを示していました。</p>
<p>参照カウントをチェックすることでキャッチされます。</p></td>
<td align="left"><p>特定のミニポートアダプターブロックのアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd netadapter</a></strong>を実行してください。</p></td>
<td align="left"><p>ドライバーによって使用されるパケット記述子のアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-pkt.md" data-raw-source="[!ndiskd.pkt](-ndiskd-pkt.md)">! ndiskd pkt</a></strong>を実行してください。</p></td>
<td align="left"><p>このパケット記述子を格納したパケット配列のアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x08</p></td>
<td align="left"><p>NDIS_BUGCHECK_HALT_WITHOUT_INTERRUPT_DEREGISTER</p>
<p>ミニポートドライバーは、停止処理中に割り込みを登録解除しませんでした。</p></td>
<td align="left"><p>特定のミニポートアダプターブロックのアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd netadapter</a></strong>を実行してください。</p></td>
<td align="left"><p>NDIS_MINIPORT_INTERRUPT のアドレス</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x09</p></td>
<td align="left"><p>NDIS_BUGCHECK_HALT_WITHOUT_CANCEL_TIMER</p>
<p>ミニポートドライバーは、すべてのタイマーを正常にキャンセルせずに停止しました。</p></td>
<td align="left"><p>特定のミニポートアダプターブロックのアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd netadapter</a></strong>を実行してください。</p></td>
<td align="left"><p>ミニポートドライバーのタイマーキューのアドレス (NDIS_MINIPORT_TIMER)</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0A</p></td>
<td align="left"><p>NDIS_BUGCHECK_DRIVER_UNLOAD_UNEXPECTED</p>
<p>ミニポートドライバーが途中でアンロードされています。</p></td>
<td align="left"><p>NDIS_M_DRIVER_BLOCK のアドレス</p></td>
<td align="left"><p>DRIVER_OBJECT のアドレス</p></td>
<td align="left"><p>ミニポートドライバーの参照カウント</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0B</p></td>
<td align="left"><p>NDIS_BUGCHECK_INIT_FAILED_WITHOUT_INTERRUPT_DEREGISTER</p>
<p>ミニポートドライバーは、割り込みを解除せずに初期化に失敗しました。</p></td>
<td align="left"><p>特定のミニポートアダプターブロックのアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd netadapter</a></strong>を実行してください。</p></td>
<td align="left"><p>NDIS_MINIPORT_INTERRUPT のアドレス</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0C</p></td>
<td align="left"><p>NDIS_BUGCHECK_INIT_FAILED_WITHOUT_CANCEL_TIMER</p>
<p>ミニポートドライバーは、すべてのタイマーを正常にキャンセルせずに初期化に失敗しました。</p></td>
<td align="left"><p>特定のミニポートアダプターブロックのアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd netadapter</a></strong>を実行してください。</p></td>
<td align="left"><p>ミニポートドライバーのタイマーキューのアドレス (NDIS_MINIPORT_TIMER)</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0D</p></td>
<td align="left"><p>NDIS_BUGCHECK_HALT_INIT_WITHOUT_INTERRUPT_DEREGISTER</p>
<p>ミニポートドライバーは、停止処理中に割り込みを登録解除しませんでした。</p>
<p>停止は、ミニポートドライバーが初期化ハンドラーから成功を返した後に、初期化ルーチンから呼び出されました。</p></td>
<td align="left"><p>特定のミニポートアダプターブロックのアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd netadapter</a></strong>を実行してください。</p></td>
<td align="left"><p>NDIS_MINIPORT_INTERRUPT のアドレス</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0E</p></td>
<td align="left"><p>NDIS_BUGCHECK_HALT_INIT_WITHOUT_CANCEL_TIMER</p>
<p>ミニポートドライバーは、すべてのタイマーを正常にキャンセルせずに停止しました。</p>
<p>停止は、ミニポートドライバーが初期化ハンドラーから成功を返した後に、初期化ルーチンから呼び出されました。</p></td>
<td align="left"><p>特定のミニポートアダプターブロックのアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd netadapter</a></strong>を実行してください。</p></td>
<td align="left"><p>ミニポートドライバーのタイマーキューのアドレス (NDIS_MINIPORT_TIMER)</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0F</p></td>
<td align="left"><p>NDIS_BUGCHECK_RESET_COMPLETE_UNEXPECTED</p>
<p><strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismresetcomplete" data-raw-source="[NdisMResetComplete](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismresetcomplete)">NdisMResetComplete</a></strong>という名前のミニポートドライバーは、保留中のリセット要求がありません。</p></td>
<td align="left"><p>特定のミニポートアダプターブロックのアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd netadapter</a></strong>を実行してください。</p></td>
<td align="left"><p>リセットの状態</p></td>
<td align="left"><p>AddressingReset (ブール値)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10</p></td>
<td align="left"><p>NDIS_BUGCHECK_PM_INIT_FAILED_NO_INT_DEREGISTER</p>
<p>低電力状態から再開した後、ミニポートドライバーは、その割り込みを解除せずに初期化に失敗しました。</p></td>
<td align="left"><p>特定のミニポートアダプターブロックのアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd netadapter</a></strong>を実行してください。</p></td>
<td align="left"><p>NDIS_MINIPORT_INTERRUPT のアドレス</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x11</p></td>
<td align="left"><p>NDIS_BUGCHECK_PM_INIT_FAILED_NO_CANCEL_TIMER</p>
<p>低電力状態から再開した後、ミニポートドライバーは、すべてのタイマーを正常にキャンセルせずに初期化に失敗しました。</p></td>
<td align="left"><p>特定のミニポートアダプターブロックのアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd netadapter</a></strong>を実行してください。</p></td>
<td align="left"><p>ミニポートドライバーのタイマーキューのアドレス (NDIS_MINIPORT_TIMER)</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x12</p></td>
<td align="left"><p>NDIS_BUGCHECK_NFILTER_RECVD_PACKET_BAD_REF_COUNT</p>
<p>ミニポートドライバーは、プロトコルスタックによって現在使用されていたパケット記述子を使用してパケットを受信したことを示しています。</p>
<p>パケット参照カウントを調べて、キャッチしました。</p></td>
<td align="left"><p>特定のミニポートアダプターブロックのアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd netadapter</a></strong>を実行してください。</p></td>
<td align="left"><p>ドライバーによって使用されるパケット記述子のアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-pkt.md" data-raw-source="[!ndiskd.pkt](-ndiskd-pkt.md)">! ndiskd pkt</a></strong>を実行してください。</p></td>
<td align="left"><p>このパケット記述子を格納したパケット配列のアドレス</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x13</p></td>
<td align="left"><p>NDIS_BUGCHECK_TFILTER_RECVD_PACKET_BAD_REF_COUNT</p>
<p>トークンリングミニポートドライバーは、プロトコルスタックによって現在使用されていたパケット記述子を使用してパケットを受信したことを示しています。</p>
<p>パケット参照カウントを調べて、キャッチしました。</p></td>
<td align="left"><p>特定のミニポートアダプターブロックのアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd netadapter</a></strong>を実行してください。</p></td>
<td align="left"><p>ドライバーによって使用されるパケット記述子のアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-pkt.md" data-raw-source="[!ndiskd.pkt](-ndiskd-pkt.md)">! ndiskd pkt</a></strong>を実行してください。</p></td>
<td align="left"><p>このパケット記述子を格納したパケット配列のアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x14</p></td>
<td align="left"><p>NDIS_BUGCHECK_WAIT_EVENT_HIGH_IRQL</p>
<p>無効な IRQL で<strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiswaitevent" data-raw-source="[NdisWaitEvent](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiswaitevent)">NdisWaitEvent</a></strong>という NDIS ドライバーが呼び出されました</p></td>
<td align="left"><p>実際の IRQL</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x15</p></td>
<td align="left"><p>NDIS_BUGCHECK_INVALID_NDIS5_CALL</p>
<p>古いドライバー用に予約されている API と呼ばれるミニポートドライバー。 ドライバーは、NDIS 6.x Api のみを呼び出す必要があります。</p></td>
<td align="left"><p>特定のミニポートアダプターブロックのアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd netadapter</a></strong>を実行してください。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x16</p></td>
<td align="left"><p>NDIS_BUGCHECK_INVALID_OPEN_IN_BIND_CONTEXT</p>
<p>プロトコルドライバーにより、バインド中にアダプターが正しく開かれませんでした。</p></td>
<td align="left"><p>特定のプロトコルのアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-protocol.md" data-raw-source="[!ndiskd.protocol](-ndiskd-protocol.md)">! ndiskd プロトコル</a></strong>を実行してください。</p></td>
<td align="left"><p>プロトコルドライバーによって割り当てられるコンテキスト領域のアドレス。</p>
<p>Ndis にキャストします。NDIS_BIND_CONTEXT.</p></td>
<td align="left"><p>開いているハンドルのアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-mopen.md" data-raw-source="[!ndiskd.mopen](-ndiskd-mopen.md)">! ndiskd mopen</a></strong>を実行してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x17</p></td>
<td align="left"><p>NDIS_BUGCHECK_IFPROVIDER_DEREGISTER_UNEXPECTED</p>
<p>最初にすべてのインターフェイスを削除せずに、 <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifderegisterprovider" data-raw-source="[NdisIfDeregisterProvider](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifderegisterprovider)">NdisIfDeregisterProvider</a></strong>というインターフェイスプロバイダーが呼び出されました。</p></td>
<td align="left"><p>インターフェイスプロバイダーハンドルのアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-ifprovider.md" data-raw-source="[!ndiskd.ifprovider](-ndiskd-ifprovider.md)">! ndiskd ifprovider</a></strong>を実行してください。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1B</p></td>
<td align="left"><p>NDIS_BUGCHECK_IF_STACK_TABLE_LOOP</p>
<p>ドライバーが ifStackTable にインターフェイスを追加しようとしましたが、これを行うと循環が発生します。 IfStackTable にはサイクルを含めることはできません。 <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifaddifstackentry" data-raw-source="[NdisIfAddIfStackEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifaddifstackentry)">NdisIfAddIfStackEntry</a></strong>を呼び出す前に、現在のテーブルを表示するには、 <strong><a href="-ndiskd-ifstacktable.md" data-raw-source="[!ndiskd.ifstacktable](-ndiskd-ifstacktable.md)">! ndiskd ifstacktable</a></strong>を実行します。</p></td>
<td align="left"><p>テーブルに追加される Higher$ Erifindex</p></td>
<td align="left"><p>テーブルに追加されているので、</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1C</p></td>
<td align="left"><p>NDIS_BUGCHECK_MINIPORT_FAILED_OID_WHICH_MUST_SUCCEED</p>
<p>ミニポートドライバーが失敗しない OID 要求に失敗しました。 そうすると、メモリやその他のリソースがリークします。</p></td>
<td align="left"><p>特定のミニポートアダプターブロックのアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd netadapter</a></strong>を実行してください。</p></td>
<td align="left"><p>失敗した OID。 この OID の名前を検索するには、 <strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">! ndiskd help</a></strong>を使用します。</p></td>
<td align="left"><p>OID 要求が完了したエラー状態コード (NDIS_STATUS_XXX)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1D</p></td>
<td align="left"><p>NDIS_BUGCHECK_OID_REQUEST_INVALID_BUFFER</p>
<p>ミニポートドライバーまたはフィルタードライバーが OID 要求を不正に完了しました。 書き込まれた BytesWritten バッファーの長さ全体を超えていないことを確認します。</p></td>
<td align="left"><p>特定のミニポートアダプターまたはフィルターモジュールブロックのアドレス。 <strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! Ndiskd netadapter</a></strong>または<strong><a href="-ndiskd-filter.md" data-raw-source="[!ndiskd.filter](-ndiskd-filter.md)">! ndiskd を実行します。</a></strong>詳細については、このアドレスを使用してフィルター処理してください。</p></td>
<td align="left"><p>不正に完了した<strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[NDIS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)">NDIS_OID_REQUEST</a></strong>へのアドレス。 <strong><a href="-ndiskd-oid.md" data-raw-source="[!ndiskd.oid](-ndiskd-oid.md)">! Ndiskd oid</a></strong>を使用して検査します。</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1E</p></td>
<td align="left"><p>NDIS_BUGCHECK_REFCOUNT_IMBALANCE</p>
<p>内部 refcount でエラーが検出されました。 これは、refcount アンダーフロー (参照よりも多くの逆参照)、またはタグの不一致によって発生することがあります。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>内部ハンドル。 <strong><a href="-ndiskd-ndisref.md" data-raw-source="[!ndiskd.ndisref](-ndiskd-ndisref.md)">! Ndiskd ndisref</a></strong>を使用するか、ndis にキャストしてください。NDIS_REFCOUNT_BLOCK.</p></td>
<td align="left"><p>現在の reftag 値</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1F</p></td>
<td align="left"><p>NDIS_BUGCHECK_ILLEGAL_MINIPORT_STATE_TRANSITION</p>
<p>ミニポートドライバーが状態遷移を正常に完了しませんでした。</p></td>
<td align="left"><p>失敗したもの。 設定可能な値:</p>
<ol>
<li><p>NDIS_BUGCHECK_ILLEGAL_MINIPORT_STATE_TRANSITION_PAUSE_COMPLETE</p>
<p>ミニポートは<strong>NdisMPauseComplete</strong>という名前ですが、保留中の一時停止操作がありませんでした。</p></li>
<li><p>NDIS_BUGCHECK_ILLEGAL_MINIPORT_STATE_TRANSITION_RESTART_COMPLETE</p>
<p>ミニポートは<strong>NdisMRestartComplete</strong>と呼ばれていますが、再起動の保留中の操作はありませんでした。</p></li>
</ol></td>
<td align="left"><p>特定のミニポートアダプターブロックのアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd netadapter</a></strong>を実行してください。</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x20</p></td>
<td align="left"><p>NDIS_BUGCHECK_STATUS_INDICATION_INVALID_BUFFER</p>
<p>ミニポートドライバーまたはフィルタードライバーに無効な<strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication" data-raw-source="[NDIS_STATUS_INDICATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)">NDIS_STATUS_INDICATION</a></strong>が指定されました。</p></td>
<td align="left"><p>ステータス表示の種類。 詳細については、このコードで<strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">! ndiskd ヘルプ</a></strong>を実行してください。</p></td>
<td align="left"><p>この無効なステータスを示すドライバーインスタンスのハンドル。 このハンドルを使用して、 <strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd netadapter</a></strong>または<strong><a href="-ndiskd-filter.md" data-raw-source="[!ndiskd.filter](-ndiskd-filter.md)">! ndiskd フィルターを実行します。</a></strong>詳細については、こちらを参照してください。</p></td>
<td align="left"><p>ステータス表示ペイロードのアドレス。 その解釈は、ステータス表示の種類によって異なります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x21</p></td>
<td align="left"><p>NDIS_BUGCHECK_INVALID_OBJECT_HEADER</p>
<p>ドライバーで無効な<strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header" data-raw-source="[NDIS_OBJECT_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)">NDIS_OBJECT_HEADER</a></strong>が作成されました。</p></td>
<td align="left"><p>無効なステータスを示すドライバーのハンドル。 詳細については、このハンドルを使用して<strong><a href="-ndiskd-minidriver.md" data-raw-source="[!ndiskd.minidriver](-ndiskd-minidriver.md)">! ndiskd. ミニドライバー</a></strong>または<strong><a href="-ndiskd-filterdriver.md" data-raw-source="[!ndiskd.filterdriver](-ndiskd-filterdriver.md)">! ndiskd. filterdriver</a></strong>を実行してください。</p></td>
<td align="left"><p>形式が正しくないヘッダーを持つオブジェクト。 その解釈は、呼び出される API によって異なります。 たとえば、ドライバーが<strong>NdisAllocateCloneOidRequest</strong>という名前の場合は、オブジェクトを ndis にキャストします。NDIS_OID_REQUEST.</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x22</p></td>
<td align="left"><p>NDIS_BUGCHECK_ILLEGAL_NET_PNP_EVENT</p>
<p>ミニポートドライバーまたはフィルタードライバーに無効な<strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification" data-raw-source="[NET_PNP_EVENT_NOTIFICATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)">NET_PNP_EVENT_NOTIFICATION</a></strong>が指定されました。</p></td>
<td align="left"><p>無効なステータスを示すドライバーのハンドル。 詳細については、このハンドルを使用して<strong><a href="-ndiskd-minidriver.md" data-raw-source="[!ndiskd.minidriver](-ndiskd-minidriver.md)">! ndiskd. ミニドライバー</a></strong>または<strong><a href="-ndiskd-filterdriver.md" data-raw-source="[!ndiskd.filterdriver](-ndiskd-filterdriver.md)">! ndiskd. filterdriver</a></strong>を実行してください。</p></td>
<td align="left"><p>NET_PNP_EVENT_NOTIFICATION にキャストする</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x23</p></td>
<td align="left"><p>NDIS_BUGCHECK_PD_ERROR</p>
<p>パケットダイレクトデータパスでエラーが検出されました。</p></td>
<td align="left"><p>バグチェックのサブタイプ。 設定可能な値:</p>
<ol>
<li><p>NDIS_BUGCHECK_PD_ERROR_EC_THREAD_MISMATCH</p>
<p>API が間違ったスレッドで呼び出されました。</p></li>
<li><p>NDIS_BUGCHECK_PD_ERROR_ILLEGAL_ARM_BY_CLIENT</p>
<p>PD クライアントが、無効な状態のときにプロバイダーを arm しようとしました。</p></li>
<li><p>NDIS_BUGCHECK_PD_ERROR_ILLEGAL_ARM_NOTIFICATION</p>
<p>PD プロバイダーは、この処理が行われていない間、不正にドレイン通知をトリガーしました。</p></li>
<li><p>NDIS_BUGCHECK_PD_ERROR_ILLEGAL_ARM_NOTIFICATION_VIA_ISR</p>
<p>PD プロバイダーは、このような処理が行われていないときに、ISR のドレイン通知を不正にトリガーしました。</p></li>
<li><p>NDIS_BUGCHECK_PD_ERROR_ILLEGAL_THUNK_BY_LWF</p>
<p>フィルタードライバーがパケットダイレクトデータパスを妨害しようとしました。</p></li>
<li><p>NDIS_BUGCHECK_PD_ERROR_ILLEGAL_BM_GROUP_REQUEST</p>
<p>PD プロバイダーがバッファーマネージャーグループから誤って削除しようとしました。</p></li>
<li><p>NDIS_BUGCHECK_PD_ERROR_ILLEGAL_PD_BUFFER_SETUP</p>
<p>PD バッファーセットアップ要求の形式が正しくありませんでした。</p></li>
</ol></td>
<td align="left"><p>パラメーター3の値は、パラメーター2の値によって異なります。 この一覧の各数値は、パラメーター2の同じ数値に対応しています。</p>
<ol>
<li>NDIS_PD_EC にキャストする</li>
<li>NDIS_PD_QUEUE_TRACKER にキャストする</li>
<li>NDIS_PD_QUEUE_TRACKER にキャストする</li>
<li>NDIS_PD_QUEUE_TRACKER にキャストする</li>
<li>特定のフィルターモジュールのハンドル。 詳細については、このハンドルを使用<strong><a href="-ndiskd-filter.md" data-raw-source="[!ndiskd.filter](-ndiskd-filter.md)">してフィルター</a></strong>を実行してください。</li>
<li>バッファーマネージャーグループ (既知の場合)</li>
<li>ソース PD_MEMORY_HANDLE または PD_BUFFER</li>
</ol></td>
<td align="left"><p>パラメーター4の値は、パラメーター2の値に依存します。 この一覧の各数値は、パラメーター2の同じ数値に対応しています。</p>
<ol>
<li>予測された ETHREAD</li>
<li>PD クライアントへのハンドル</li>
<li>PD プロバイダーへのハンドル。 詳細については、このハンドルで<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd netadapter</a></strong>を実行してください。</li>
<li>PD プロバイダーへのハンドル。 詳細については、このハンドルで<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd netadapter</a></strong>を実行してください。</li>
<li>PD プロバイダーへのハンドル。 詳細については、このハンドルで<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd netadapter</a></strong>を実行してください。</li>
<li><p>パラメーター3が0の場合、これはプロバイダーハンドルです。</p>
<p>パラメーター3が0以外の場合、PD クライアントは、まだすべての割り当てを解放していません。これは、PD クライアントハンドルです。</p></li>
<li>ターゲット PD_BUFFER</li>
</ol></td>
</tr>
<tr class="odd">
<td align="left"><p>0x24</p></td>
<td align="left"><p>NDIS_BUGCHECK_UNEXPECTED_FAILURE</p>
<p>内部操作が予期せず失敗しました。 これは、NDIS のバグである可能性があります。システム自体。</p></td>
<td align="left"><p>失敗した操作。 設定可能な値:</p>
<p>0x01: NDIS_BUGCHECK_UNEXPECTED_FAILURE_KEWAITFORSINGLEOBJECT</p>
<p>KeWaitForSingleObject の呼び出しに失敗しました。</p></td>
<td align="left"><p>エラー状態コード</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x25</p></td>
<td align="left"><p>NDIS_BUGCHECK_WATCHDOG</p>
<p>ネットワークスタックを管理しようとしましたが、時間がかかりすぎています。 NDIS は他のドライバーを呼び出すと、呼び出しが即座に完了するようにウォッチドッグタイマーを開始します。 呼び出しに時間がかかる場合、NDIS はバグチェックを挿入します。</p>
<p>これは、単純なデッドロックが原因である可能性があります。 "! Stack 2 ndis" を使用するか、疑わしいと思われるスレッドがあるかどうかを確認します。 NDIS_WATCHDOG_TRIAGE_BLOCK から PrimaryThread に特に注意を払ってください。</p>
<p>NBLs が失われたことが原因である可能性があります。その場合は、 <strong><a href="-ndiskd-pendingnbls.md" data-raw-source="[!ndiskd.pendingnbls](-ndiskd-pendingnbls.md)">pendingnbls</a></strong>が役に立ちます。 <strong><a href="-ndiskd-oid.md" data-raw-source="[!ndiskd.oid](-ndiskd-oid.md)">! Ndiskd oid</a></strong>を使用してスタックされている oid を確認します。</p></td>
<td align="left"><p>操作に時間がかかりすぎました。 設定可能な値:</p>
<ul>
<li><p>0x01: NDIS_BUGCHECK_WATCHDOG_PROTOCOL_PAUSE</p>
<p>プロトコルドライバーの一時停止中にタイムアウトが発生しました。</p></li>
<li><p>0x02: NDIS_BUGCHECK_WATCHDOG_PROTOCOL_NETPNPEVENT</p>
<p>プロトコルドライバーに NET_PNP_EVENT_NOTIFICATION を配信中にタイムアウトが発生しました。</p></li>
<li><p>0x03: NDIS_BUGCHECK_WATCHDOG_PROTOCOL_STATUS_INDICATION</p>
<p>プロトコルドライバーに状態の通知を配信中にタイムアウトが発生しました。</p></li>
<li><p>0x04: NDIS_BUGCHECK_WATCHDOG_PROTOCOL_UNBIND</p>
<p>プロトコルドライバーのバインド解除中にタイムアウトが発生しました。</p></li>
<li><p>0x11 : NDIS_BUGCHECK_WATCHDOG_FILTER_PAUSE</p>
<p>フィルタードライバーの一時停止中にタイムアウトが発生しました。</p></li>
<li><p>0x12 : NDIS_BUGCHECK_WATCHDOG_FILTER_NETPNPEVENT</p>
<p>フィルタードライバーに NET_PNP_EVENT_NOTIFICATION を配信中にタイムアウトが発生しました。</p></li>
<li><p>0x13: NDIS_BUGCHECK_WATCHDOG_FILTER_STATUS_INDICATION</p>
<p>フィルタードライバーへのステータスの通知を配信中にタイムアウトが発生しました。</p></li>
<li><p>0x14: NDIS_BUGCHECK_WATCHDOG_FILTER_DETACH</p>
<p>フィルタードライバーのデタッチ中にタイムアウトが発生しました。</p></li>
<li><p>0x21: NDIS_BUGCHECK_WATCHDOG_MINIPORT_PAUSE</p>
<p>ミニポートアダプターの一時停止中にタイムアウトが発生しました。</p></li>
<li><p>0x22: NDIS_BUGCHECK_WATCHDOG_MINIPORT_HALT</p>
<p>ミニポートアダプターの停止中にタイムアウトが発生しました。</p></li>
<li><p>0x23: NDIS_BUGCHECK_WATCHDOG_MINIPORT_OID</p>
<p>ミニポートアダプターに OID 要求を配信中にタイムアウトが発生しました。</p></li>
<li><p>0x24: NDIS_BUGCHECK_WATCHDOG_FILTER_OID</p>
<p>フィルタードライバーに OID 要求を配信中にタイムアウトが発生しました。</p></li>
<li><p>0x25: NDIS_BUGCHECK_WATCHDOG_MINIPORT_IDLE</p>
<p>ミニポートアダプターのアイドル状態中にタイムアウトが発生しました。</p></li>
<li><p>0x26: NDIS_BUGCHECK_WATCHDOG_CANCEL_IDLE</p>
<p>ミニポートアダプターでアイドル状態の要求を取り消しているときにタイムアウトが発生しました。</p></li>
</ul></td>
<td align="left"><p>Ndis にキャストします。NDIS_WATCHDOG_TRIAGE_BLOCK. 便利なフィールド:</p>
<ul>
<li><strong>StartTime</strong>は、KeQueryInterruptTime によって返される操作の開始時刻を100ナノ秒単位で表示します。</li>
<li><strong>Timeoutmilliseconds</strong>は、このバグチェックをトリガーする前に、少なくとも NDIS が待機した時間を示します。</li>
<li><strong>TargetObject</strong>は、NDIS が待機しているプロトコル、フィルターモジュール、またはミニポートアダプターへのハンドルです。 詳細については、このハンドルを使用して<strong><a href="-ndiskd-protocol.md" data-raw-source="[!ndiskd.protocol](-ndiskd-protocol.md)">! ndiskd protocol</a></strong>、 <strong><a href="-ndiskd-filter.md" data-raw-source="[!ndiskd.filter](-ndiskd-filter.md)">! ndiskd filter</a></strong>、または<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd netadapter</a></strong>を実行してください。</li>
<li><strong>Primarythread</strong>は、NDIS が操作を開始したスレッドです。 通常、これは最初に確認する場所ですが、操作が非同期に処理されている場合、スレッドは他の場所に存在する可能性があります。</li>
</ul></td>
<td align="left"><p>パラメーター4の値は、パラメーター2の値に依存します。 この一覧の各数値は、パラメーター2の同じ16進値に対応しています。</p>
<ul>
<li>0x01: 0</li>
<li>0x02: スタックイベントの NET_PNP_EVENT_CODE。 これらのコードの詳細については、「 <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event" data-raw-source="[NET_PNP_EVENT](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event)">NET_PNP_EVENT</a></strong>.」を参照してください。</li>
<li>0x03: スタック表示の NDIS_STATUS コード。 <strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">! Ndiskd help</a></strong>を使用してデコードしてください。</li>
<li>0x04: 0</li>
<li>0x11: 0</li>
<li>0x12: スタックイベントの NET_PNP_EVENT_CODE。 使用可能な値については、この一覧の項目2の値の前の一覧を参照してください。</li>
<li>0x13: スタック表示の NDIS_STATUS コード。 <strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">! Ndiskd help</a></strong>を使用してデコードしてください。</li>
<li>0x14: 0</li>
<li>0x21: 0</li>
<li>0x22: 0</li>
<li>0x23: スタック要求の OID コード。 <strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">! Ndiskd help</a></strong>を使用してデコードしてください。</li>
<li>0x24: スタック要求の OID コード。 <strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">! Ndiskd help</a></strong>を使用してデコードしてください。</li>
<li>0x25: 0</li>
<li>0x26: 0</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p>0x26</p></td>
<td align="left"><p>NDIS_BUGCHECK_INVALID_OID_COMPLETION</p>
<p>ミニポートドライバーが、そのミニポートドライバーで現在保留されていない OID 要求を完了しようとしました。 これは、ドライバーが同じ要求を複数回実行しようとした場合に発生する可能性があります。</p></td>
<td align="left"><p>バグチェックの原因となったミニポートドライバーハンドル。 詳細については、このハンドルで<strong><a href="-ndiskd-minidriver.md" data-raw-source="[!ndiskd.minidriver](-ndiskd-minidriver.md)">! ndiskd</a></strong>を実行してください。</p></td>
<td align="left"><p>ミニポートドライバーが完了しようとしている NDIS OID 要求。 この要求で<strong><a href="-ndiskd-oid.md" data-raw-source="[!ndiskd.oid](-ndiskd-oid.md)">! ndiskd oid</a></strong>を実行しようとすることはできますが、この時点ではメモリが有効ではない可能性があります。</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x27</p></td>
<td align="left"><p>NDIS_BUGCHECK_LEAKED_NBL</p>
<p>ドライバーが<strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list" data-raw-source="[NET_BUFFER_LIST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)">NET_BUFFER_LIST</a></strong>構造体をリークしています。 このドライバーでまだ保留中の NBLs を確認するには、 <strong><a href="-ndiskd-pendingnbls.md" data-raw-source="[!ndiskd.pendingnbls](-ndiskd-pendingnbls.md)">! ndiskd</a></strong>を使用してください。</p></td>
<td align="left"><p>リークが検出された場所。 設定可能な値:</p>
<ul>
<li><p>0x01: NBL tracker によってリークが検出されました。 現在登録解除またはバインド解除されているドライバーは、最も可能性の高い原因です。 バグチェックスレッドの呼び出し履歴を確認します。 ドライバーは、アクティブな NBLs を保持したまま、バインド解除または登録解除を行うことはできません。</p></li>
</ul></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

パラメーター1は、バグコード\_NDIS\_ドライバーのバグチェックの具体的な原因を示します。

<a name="remarks"></a>注釈
-------

バグコード\_NDIS\_ドライバーは、ネットワークドライバーで indendifies の問題をチェックします。 多くの場合、この問題は NDIS ミニポートドライバーによって発生します。 すべての NDIS ミニポートドライバーの一覧を取得するには、 [ **! ndiskd netadapter**](-ndiskd-netadapter.md)を使用します。 ネットワークスタックの概要を確認するには、 [ **! ndiskd netreport**](-ndiskd-netreport.md)を使用します。

このバグチェックコードは、Microsoft Windows Server 2003 以降のバージョンの Windows でのみ発生します。 Windows 2000 および Windows XP では、対応するコードは[**バグチェック 0xD2 (バグ**](bug-check-0xd2--bugcode-id-driver.md)コード\_ID\_ドライバー) です。

 

 




