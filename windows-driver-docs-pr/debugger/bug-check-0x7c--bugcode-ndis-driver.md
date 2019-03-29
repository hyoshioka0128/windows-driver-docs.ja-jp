---
title: バグ チェック 0x7C BUGCODE_NDIS_DRIVER
description: BUGCODE_NDIS_DRIVER のバグ チェックでは、0x0000007C の値を持ちます。 このバグ チェックでは、オペレーティング システムに、ネットワークのドライバーでエラーが検出されたことを示します。
ms.assetid: 0f2c2e9c-2889-4d99-b653-0ee1d4c2be0e
keywords:
- バグ チェック 0x7C BUGCODE_NDIS_DRIVER
- BUGCODE_NDIS_DRIVER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BUGCODE_NDIS_DRIVER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c3b0d9046aa564a00f6b33ff4b27abf1a23c6a52
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57463944"
---
# <a name="bug-check-0x7c-bugcodendisdriver"></a>バグ チェック 0x7C:BUGCODE\_NDIS\_ドライバー


BUGCODE\_NDIS\_ドライバーのバグ チェックが 0x0000007C の値を持ちます。 このバグ チェックでは、オペレーティング システムに、ネットワークのドライバーでエラーが検出されたことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="bugcodendisdriver-parameters"></a>BUGCODE\_NDIS\_ドライバーのパラメーター


パラメーター 1 では、違反の種類を示します。 その他のパラメーターの意味は、パラメーター 1 の値によって異なります。 つまり、パラメーターの値が「0」の場合はは使用されません。

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
<th align="left">パラメーター 1</th>
<th align="left">パラメーター 1 の値とエラーの原因</th>
<th align="left">パラメータ 2</th>
<th align="left">3 番目のパラメーター</th>
<th align="left">パラメーター 4</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>NDIS_BUGCHECK_ALLOCATE_SHARED_MEM_HIGH_IRQL</p>
<p>ドライバーと呼ばれる<strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff562782" data-raw-source="[NdisMAllocateSharedMemory](https://msdn.microsoft.com/library/windows/hardware/ff562782)">NdisMAllocateSharedMemory</a></strong>なります。</p></td>
<td align="left"><p>特定のミニポート アダプター ブロックのアドレス。 実行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd.netadapter</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>要求された共有メモリの長さ</p></td>
<td align="left"><p>現在の IRQL</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>NDIS_BUGCHECK_SHARED_MEM_CORRUPTION</p>
<p>呼び出し中に <strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff562782" data-raw-source="[NdisMAllocateSharedMemory](https://msdn.microsoft.com/library/windows/hardware/ff562782)">NdisMAllocateSharedMemory</a></strong>NDIS は、共有メモリを以前に割り当てられたページが破損していたことが検出されました。</p></td>
<td align="left"><p>特定のミニポート アダプター ブロックのアドレス。 実行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd.netadapter</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>共有メモリ ページが破損しています。</p></td>
<td align="left"><p>共有メモリの割り当て、ドライバーでの追跡を NDIS_WRAPPER_CONTEXTE のアドレス</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03</p></td>
<td align="left"><p>NDIS_BUGCHECK_FREE_INVALID_SHARED_MEM</p>
<p>ミニポート ドライバーと呼ばれます<strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff563589" data-raw-source="[NdisMFreeSharedMemory](https://msdn.microsoft.com/library/windows/hardware/ff563589)">NdisMFreeSharedMemory</a></strong> (<strong>Async</strong>) が既に解放されて共有メモリ アドレスを使用します。</p></td>
<td align="left"><p>特定のミニポート アダプター ブロックのアドレス。 実行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd.netadapter</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>この共有メモリの割り当てられたページ</p></td>
<td align="left"><p>共有メモリの仮想アドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x04</p></td>
<td align="left"><p>NDIS_BUGCHECK_UNLOAD_DRIVER_INVALID_PARAMETER</p>
<p><strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff540521" data-raw-source="[AddDevice](https://msdn.microsoft.com/library/windows/hardware/ff540521)">AddDevice</a></strong>  NDIS に登録されているドライバーの一覧ではないにドライバーが呼び出されました。</p>
<p>特別なインストルメント化された NDIS でのみ有効にします。</p></td>
<td align="left"><p>NDIS_M_DRIVER_BLOCK のアドレス</p></td>
<td align="left"><p>DRIVER_OBJECT のアドレス</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x05</p></td>
<td align="left"><p>NDIS_BUGCHECK_RECVD_PACKET_IN_USE_BAD_STACK_LOCATION</p>
<p>イーサネット ドライバーには、プロトコル スタックで使用されていたパケット記述子を使用してパケットを受信することが示されます。</p>
<p>スタックのパケットの場所を確認することによってキャッチされます。</p></td>
<td align="left"><p>特定のミニポート アダプター ブロックのアドレス。 実行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd.netadapter</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>ドライバーで使用されるパケットの記述子のアドレス。 実行<strong><a href="-ndiskd-pkt.md" data-raw-source="[!ndiskd.pkt](-ndiskd-pkt.md)">! ndiskd.pkt</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>このパケット記述子を含むパケットの配列のアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x06</p></td>
<td align="left"><p>NDIS_BUGCHECK_RECVD_PACKET_IN_USE_BAD_REF_COUNT</p>
<p>イーサネット ドライバーには、プロトコル スタックで使用されていたパケット記述子を使用してパケットを受信することが示されます。</p>
<p>パケットの参照カウントのチェックをキャッチします。</p></td>
<td align="left"><p>特定のミニポート アダプター ブロックのアドレス。 実行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd.netadapter</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>ドライバーで使用されるパケットの記述子のアドレス。 実行<strong><a href="-ndiskd-pkt.md" data-raw-source="[!ndiskd.pkt](-ndiskd-pkt.md)">! ndiskd.pkt</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>このパケット記述子を含むパケットの配列のアドレス</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x07</p></td>
<td align="left"><p>プロトコル スタックで使用されていたパケット記述子を使用してパケットを受信しましたが、FDDI ドライバーが示されます。</p>
<p>参照カウントのチェックをキャッチします。</p></td>
<td align="left"><p>特定のミニポート アダプター ブロックのアドレス。 実行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd.netadapter</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>ドライバーで使用されるパケットの記述子のアドレス。 実行<strong><a href="-ndiskd-pkt.md" data-raw-source="[!ndiskd.pkt](-ndiskd-pkt.md)">! ndiskd.pkt</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>このパケット記述子を含むパケットの配列のアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x08</p></td>
<td align="left"><p>NDIS_BUGCHECK_HALT_WITHOUT_INTERRUPT_DEREGISTER</p>
<p>ミニポート ドライバーは、その割り込みが停止処理中に登録解除できませんでした。</p></td>
<td align="left"><p>特定のミニポート アダプター ブロックのアドレス。 実行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd.netadapter</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>NDIS_MINIPORT_INTERRUPT のアドレス</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x09</p></td>
<td align="left"><p>NDIS_BUGCHECK_HALT_WITHOUT_CANCEL_TIMER</p>
<p>正常にそのすべてのタイマーをキャンセルせずに、ミニポート ドライバーが停止しました。</p></td>
<td align="left"><p>特定のミニポート アダプター ブロックのアドレス。 実行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd.netadapter</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>ミニポート ドライバーのタイマー キュー (NDIS_MINIPORT_TIMER) のアドレス</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0A</p></td>
<td align="left"><p>NDIS_BUGCHECK_DRIVER_UNLOAD_UNEXPECTED</p>
<p>ミニポート ドライバーが途中でアンロードを取得します。</p></td>
<td align="left"><p>NDIS_M_DRIVER_BLOCK のアドレス</p></td>
<td align="left"><p>DRIVER_OBJECT のアドレス</p></td>
<td align="left"><p>ミニポート ドライバーの参照カウント</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0B</p></td>
<td align="left"><p>NDIS_BUGCHECK_INIT_FAILED_WITHOUT_INTERRUPT_DEREGISTER</p>
<p>ミニポート ドライバーでは、その割り込みの登録を解除せず、初期化できませんでした。</p></td>
<td align="left"><p>特定のミニポート アダプター ブロックのアドレス。 実行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd.netadapter</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>NDIS_MINIPORT_INTERRUPT のアドレス</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0C</p></td>
<td align="left"><p>NDIS_BUGCHECK_INIT_FAILED_WITHOUT_CANCEL_TIMER</p>
<p>ミニポート ドライバーでは、正常にそのすべてのタイマーをキャンセルせず、初期化できませんでした。</p></td>
<td align="left"><p>特定のミニポート アダプター ブロックのアドレス。 実行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd.netadapter</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>ミニポート ドライバーのタイマー キュー (NDIS_MINIPORT_TIMER) のアドレス</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0D</p></td>
<td align="left"><p>NDIS_BUGCHECK_HALT_INIT_WITHOUT_INTERRUPT_DEREGISTER</p>
<p>ミニポート ドライバーは、その割り込みが停止処理中に登録解除できませんでした。</p>
<p>ミニポート ドライバーでは、その初期化ハンドラーから成功が返された後、初期化ルーチンから halt が呼び出されました。</p></td>
<td align="left"><p>特定のミニポート アダプター ブロックのアドレス。 実行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd.netadapter</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>NDIS_MINIPORT_INTERRUPT のアドレス</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0E</p></td>
<td align="left"><p>NDIS_BUGCHECK_HALT_INIT_WITHOUT_CANCEL_TIMER</p>
<p>正常にそのすべてのタイマーをキャンセルせずに、ミニポート ドライバーが停止しました。</p>
<p>ミニポート ドライバーでは、その初期化ハンドラーから成功が返された後、初期化ルーチンから halt が呼び出されました。</p></td>
<td align="left"><p>特定のミニポート アダプター ブロックのアドレス。 実行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd.netadapter</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>ミニポート ドライバーのタイマー キュー (NDIS_MINIPORT_TIMER) のアドレス</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0F</p></td>
<td align="left"><p>NDIS_BUGCHECK_RESET_COMPLETE_UNEXPECTED</p>
<p>ミニポート ドライバーと呼ばれます<strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff563663" data-raw-source="[NdisMResetComplete](https://msdn.microsoft.com/library/windows/hardware/ff563663)">NdisMResetComplete</a></strong>任意の保留中のリセットの要求なし。</p></td>
<td align="left"><p>特定のミニポート アダプター ブロックのアドレス。 実行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd.netadapter</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>リセットの状態</p></td>
<td align="left"><p>AddressingReset (BOOLEAN)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10</p></td>
<td align="left"><p>NDIS_BUGCHECK_PM_INIT_FAILED_NO_INT_DEREGISTER</p>
<p>低電力状態から再開すた後、ミニポート ドライバーは、割り込みの登録を解除せず、初期化できませんでした。</p></td>
<td align="left"><p>特定のミニポート アダプター ブロックのアドレス。 実行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd.netadapter</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>NDIS_MINIPORT_INTERRUPT のアドレス</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x11</p></td>
<td align="left"><p>NDIS_BUGCHECK_PM_INIT_FAILED_NO_CANCEL_TIMER</p>
<p>低電力状態から再開すた後、ミニポート ドライバーを正常にそのすべてのタイマーをキャンセルせず、初期化できませんでした。</p></td>
<td align="left"><p>特定のミニポート アダプター ブロックのアドレス。 実行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd.netadapter</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>ミニポート ドライバーのタイマー キュー (NDIS_MINIPORT_TIMER) のアドレス</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x12</p></td>
<td align="left"><p>NDIS_BUGCHECK_NFILTER_RECVD_PACKET_BAD_REF_COUNT</p>
<p>ミニポート ドライバーには、プロトコル スタックで使用されていたパケット記述子を使用してパケットを受信することが示されます。</p>
<p>パケットの参照カウントのチェックをキャッチします。</p></td>
<td align="left"><p>特定のミニポート アダプター ブロックのアドレス。 実行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd.netadapter</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>ドライバーで使用されるパケットの記述子のアドレス。 実行<strong><a href="-ndiskd-pkt.md" data-raw-source="[!ndiskd.pkt](-ndiskd-pkt.md)">! ndiskd.pkt</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>このパケット記述子を含むパケットの配列のアドレス</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x13</p></td>
<td align="left"><p>NDIS_BUGCHECK_TFILTER_RECVD_PACKET_BAD_REF_COUNT</p>
<p>トークン リングのミニポート ドライバーには、プロトコル スタックで使用されていたパケット記述子を使用してパケットを受信することが示されます。</p>
<p>パケットの参照カウントのチェックをキャッチします。</p></td>
<td align="left"><p>特定のミニポート アダプター ブロックのアドレス。 実行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd.netadapter</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>ドライバーで使用されるパケットの記述子のアドレス。 実行<strong><a href="-ndiskd-pkt.md" data-raw-source="[!ndiskd.pkt](-ndiskd-pkt.md)">! ndiskd.pkt</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>このパケット記述子を含むパケットの配列のアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x14</p></td>
<td align="left"><p>NDIS_BUGCHECK_WAIT_EVENT_HIGH_IRQL</p>
<p>NDIS ドライバーと呼ばれる<strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff564651" data-raw-source="[NdisWaitEvent](https://msdn.microsoft.com/library/windows/hardware/ff564651)">NdisWaitEvent</a></strong>不正な IRQL で</p></td>
<td align="left"><p>実際の IRQL</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x15</p></td>
<td align="left"><p>NDIS_BUGCHECK_INVALID_NDIS5_CALL</p>
<p>ミニポート ドライバーでは、古いバージョンのドライバー用に予約されている API が呼び出されます。 ドライバーは、NDIS を呼び出す必要がありますのみ 6.x Api。</p></td>
<td align="left"><p>特定のミニポート アダプター ブロックのアドレス。 実行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd.netadapter</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x16</p></td>
<td align="left"><p>NDIS_BUGCHECK_INVALID_OPEN_IN_BIND_CONTEXT</p>
<p>プロトコル ドライバーは、バインド中に不適切なアダプターを開きます。</p></td>
<td align="left"><p>特定のプロトコルのアドレス。 実行<strong><a href="-ndiskd-protocol.md" data-raw-source="[!ndiskd.protocol](-ndiskd-protocol.md)">! ndiskd.protocol</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>プロトコル ドライバーが割り当てられるコンテキスト領域のアドレス。</p>
<p>Ndis にキャストされます。NDIS_BIND_CONTEXT します。</p></td>
<td align="left"><p>開いているハンドルのアドレス。 実行<strong><a href="-ndiskd-mopen.md" data-raw-source="[!ndiskd.mopen](-ndiskd-mopen.md)">! ndiskd.mopen</a></strong>詳細については、このアドレスを使用します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x17</p></td>
<td align="left"><p>NDIS_BUGCHECK_IFPROVIDER_DEREGISTER_UNEXPECTED</p>
<p>インターフェイスをプロバイダーと呼ばれる<strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff562703" data-raw-source="[NdisIfDeregisterProvider](https://msdn.microsoft.com/library/windows/hardware/ff562703)">NdisIfDeregisterProvider</a></strong>最初に、そのすべてのインターフェイスを削除します。</p></td>
<td align="left"><p>インターフェイスのプロバイダーのハンドルのアドレス。 実行<strong><a href="-ndiskd-ifprovider.md" data-raw-source="[!ndiskd.ifprovider](-ndiskd-ifprovider.md)">! ndiskd.ifprovider</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1B</p></td>
<td align="left"><p>NDIS_BUGCHECK_IF_STACK_TABLE_LOOP</p>
<p>ドライバーは、ifStackTable にインターフェイスを追加しようとしていますが、サイクルが発生するとします。 IfStackTable いないサイクルが必要です。 実行<strong><a href="-ndiskd-ifstacktable.md" data-raw-source="[!ndiskd.ifstacktable](-ndiskd-ifstacktable.md)">! ndiskd.ifstacktable</a></strong>を現在のテーブルを参照してください (この呼び出しの前に <strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff562693" data-raw-source="[NdisIfAddIfStackEntry](https://msdn.microsoft.com/library/windows/hardware/ff562693)">NdisIfAddIfStackEntry</a></strong>)。</p></td>
<td align="left"><p>テーブルに追加されている HigherLayerIfIndex</p></td>
<td align="left"><p>テーブルに追加されている LowerLayerIfIndex</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1C</p></td>
<td align="left"><p>NDIS_BUGCHECK_MINIPORT_FAILED_OID_WHICH_MUST_SUCCEED</p>
<p>ミニポート ドライバーには、失敗する必要がありますいないした OID 要求が失敗しました。 これにより、メモリまたはその他のリソースがリークします。</p></td>
<td align="left"><p>特定のミニポート アダプター ブロックのアドレス。 実行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd.netadapter</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>この OID が失敗しました。 使用<strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">! ndiskd.help</a></strong>この OID の名前を検索します。</p></td>
<td align="left"><p>OID 要求が完了したがエラー状態コード (NDIS_STATUS_XXX)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1D</p></td>
<td align="left"><p>NDIS_BUGCHECK_OID_REQUEST_INVALID_BUFFER</p>
<p>ミニポート ドライバーまたはフィルター ドライバーが完了した OID 要求を不正にします。 BytesWritten がバッファーの全体の長さを超えていないことを確認します。</p></td>
<td align="left"><p>特定のミニポート アダプターまたはフィルター モジュールのブロックのアドレス。 実行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd.netadapter</a></strong>または<strong><a href="-ndiskd-filter.md" data-raw-source="[!ndiskd.filter](-ndiskd-filter.md)">! ndiskd.filter</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>アドレスを<strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff566710" data-raw-source="[NDIS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/ff566710)">NDIS_OID_REQUEST</a></strong>不法を完了しました。 検査で <strong><a href="-ndiskd-oid.md" data-raw-source="[!ndiskd.oid](-ndiskd-oid.md)">! ndiskd.oid</a></strong>します。</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1E</p></td>
<td align="left"><p>NDIS_BUGCHECK_REFCOUNT_IMBALANCE</p>
<p>NDIS 内部の参照カウントのエラーが検出されました。 これは、(より詳細は逆参照) refcount アンダー フロー、またはタグの不一致によって発生することができます。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>内部ハンドル。 使用<strong><a href="-ndiskd-ndisref.md" data-raw-source="[!ndiskd.ndisref](-ndiskd-ndisref.md)">! ndiskd.ndisref</a></strong>または ndis へのキャストです。NDIS_REFCOUNT_BLOCK します。</p></td>
<td align="left"><p>現在の reftag 値</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1F</p></td>
<td align="left"><p>NDIS_BUGCHECK_ILLEGAL_MINIPORT_STATE_TRANSITION</p>
<p>ミニポート ドライバーでは、不正に状態遷移を完了します。</p></td>
<td align="left"><p>何が失敗しました。 設定可能な値:</p>
<ol>
<li><p>NDIS_BUGCHECK_ILLEGAL_MINIPORT_STATE_TRANSITION_PAUSE_COMPLETE</p>
<p>ミニポートと呼ばれる<strong>NdisMPauseComplete</strong>保留中の一時停止操作がありませんでした。</p></li>
<li><p>NDIS_BUGCHECK_ILLEGAL_MINIPORT_STATE_TRANSITION_RESTART_COMPLETE</p>
<p>ミニポートと呼ばれる<strong>NdisMRestartComplete</strong>保留中の再起動操作がありませんでした。</p></li>
</ol></td>
<td align="left"><p>特定のミニポート アダプター ブロックのアドレス。 実行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd.netadapter</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x20</p></td>
<td align="left"><p>NDIS_BUGCHECK_STATUS_INDICATION_INVALID_BUFFER</p>
<p>ミニポート ドライバーまたはフィルター ドライバーに不正なが示される <strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff567373" data-raw-source="[NDIS_STATUS_INDICATION](https://msdn.microsoft.com/library/windows/hardware/ff567373)">NDIS_STATUS_INDICATION</a></strong>します。</p></td>
<td align="left"><p>状態表示の型。 実行<strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">! ndiskd.help</a></strong>詳細については、このコードを使用します。</p></td>
<td align="left"><p>この無効な状態を示す値を指定するドライバーのインスタンスのハンドル。 実行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd.netadapter</a></strong>または<strong><a href="-ndiskd-filter.md" data-raw-source="[!ndiskd.filter](-ndiskd-filter.md)">! ndiskd.filter</a></strong>詳細については、このハンドルを使用します。</p></td>
<td align="left"><p>状態を示す値のペイロードのアドレス。 その解釈は、状態表示の種類によって異なります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x21</p></td>
<td align="left"><p>NDIS_BUGCHECK_INVALID_OBJECT_HEADER</p>
<p>ドライバーの作成、無効な <strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff566588" data-raw-source="[NDIS_OBJECT_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff566588)">NDIS_OBJECT_HEADER</a></strong>します。</p></td>
<td align="left"><p>無効な状態の表示を示す、ドライバーのハンドル。 実行<strong><a href="-ndiskd-minidriver.md" data-raw-source="[!ndiskd.minidriver](-ndiskd-minidriver.md)">! ndiskd.minidriver</a></strong>または<strong><a href="-ndiskd-filterdriver.md" data-raw-source="[!ndiskd.filterdriver](-ndiskd-filterdriver.md)">! ndiskd.filterdriver</a></strong>詳細については、このハンドルを使用します。</p></td>
<td align="left"><p>正しくない形式のヘッダーを持つオブジェクト。 その解釈は、呼び出される API に依存します。 たとえば、ドライバーと呼ばれる<strong>NdisAllocateCloneOidRequest</strong>ndis をオブジェクトにキャストし、!NDIS_OID_REQUEST します。</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x22</p></td>
<td align="left"><p>NDIS_BUGCHECK_ILLEGAL_NET_PNP_EVENT</p>
<p>ミニポート ドライバーまたはフィルター ドライバーに不正なが示される <strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff568752" data-raw-source="[NET_PNP_EVENT_NOTIFICATION](https://msdn.microsoft.com/library/windows/hardware/ff568752)">NET_PNP_EVENT_NOTIFICATION</a></strong>します。</p></td>
<td align="left"><p>無効な状態の表示を示す、ドライバーのハンドル。 実行<strong><a href="-ndiskd-minidriver.md" data-raw-source="[!ndiskd.minidriver](-ndiskd-minidriver.md)">! ndiskd.minidriver</a></strong>または<strong><a href="-ndiskd-filterdriver.md" data-raw-source="[!ndiskd.filterdriver](-ndiskd-filterdriver.md)">! ndiskd.filterdriver</a></strong>詳細については、このハンドルを使用します。</p></td>
<td align="left"><p>NET_PNP_EVENT_NOTIFICATION にキャスト</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x23</p></td>
<td align="left"><p>NDIS_BUGCHECK_PD_ERROR</p>
<p>パケット ダイレクト データパスでエラーが検出されました。</p></td>
<td align="left"><p>バグチェックのサブタイプ。 設定可能な値:</p>
<ol>
<li><p>NDIS_BUGCHECK_PD_ERROR_EC_THREAD_MISMATCH</p>
<p>API は、間違ったスレッドで呼び出されました。</p></li>
<li><p>NDIS_BUGCHECK_PD_ERROR_ILLEGAL_ARM_BY_CLIENT</p>
<p>PD クライアントは、無効な状態のとき、プロバイダーを arm しようとしました。</p></li>
<li><p>NDIS_BUGCHECK_PD_ERROR_ILLEGAL_ARM_NOTIFICATION</p>
<p>PD プロバイダーでは、武装ことがないときに、不正にドレイン通知がトリガーされます。</p></li>
<li><p>NDIS_BUGCHECK_PD_ERROR_ILLEGAL_ARM_NOTIFICATION_VIA_ISR</p>
<p>PD プロバイダーでは、武装ことがないときに、ISR ドレイン通知が不正にトリガーされます。</p></li>
<li><p>NDIS_BUGCHECK_PD_ERROR_ILLEGAL_THUNK_BY_LWF</p>
<p>フィルター ドライバーでは、パケット ダイレクト データパス干渉しようとしています。</p></li>
<li><p>NDIS_BUGCHECK_PD_ERROR_ILLEGAL_BM_GROUP_REQUEST</p>
<p>PD プロバイダーは、不正にバッファー マネージャーのグループからそれ自体を削除しようとします。</p></li>
<li><p>NDIS_BUGCHECK_PD_ERROR_ILLEGAL_PD_BUFFER_SETUP</p>
<p>PD バッファー セットアップの要求が正しくありません。</p></li>
</ol></td>
<td align="left"><p>パラメーター 3 の値は、パラメーター 2 の値によって異なります。 この一覧の各番号は、パラメーター 2 で同じ番号に対応します。</p>
<ol>
<li>NDIS_PD_EC にキャスト</li>
<li>NDIS_PD_QUEUE_TRACKER にキャスト</li>
<li>NDIS_PD_QUEUE_TRACKER にキャスト</li>
<li>NDIS_PD_QUEUE_TRACKER にキャスト</li>
<li>特定のフィルター モジュールのハンドル。 実行<strong><a href="-ndiskd-filter.md" data-raw-source="[!ndiskd.filter](-ndiskd-filter.md)">! ndiskd.filter</a></strong>詳細については、このハンドルを使用します。</li>
<li>既知の場合、バッファー マネージャー グループ</li>
<li>PD_MEMORY_HANDLE または PD_BUFFER ソース</li>
</ol></td>
<td align="left"><p>パラメーター 4 の値は、パラメーター 2 の値によって異なります。 この一覧の各番号は、パラメーター 2 で同じ番号に対応します。</p>
<ol>
<li>必要があった ETHREAD</li>
<li>PD クライアントを識別するハンドル</li>
<li>PD プロバイダーへのハンドル。 実行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd.netadapter</a></strong>詳細については、このハンドルを使用します。</li>
<li>PD プロバイダーへのハンドル。 実行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd.netadapter</a></strong>詳細については、このハンドルを使用します。</li>
<li>PD プロバイダーへのハンドル。 実行<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd.netadapter</a></strong>詳細については、このハンドルを使用します。</li>
<li><p>パラメーター 3 が 0 の場合は、これは、プロバイダーのハンドル。</p>
<p>パラメーター 3 が 0 以外の場合は、PD クライアントがすべての割り当てをまだ、解放しないと PD クライアント ハンドルします。</p></li>
<li>ターゲット PD_BUFFER</li>
</ol></td>
</tr>
<tr class="odd">
<td align="left"><p>0x24</p></td>
<td align="left"><p>NDIS_BUGCHECK_UNEXPECTED_FAILURE</p>
<p>内部の操作に失敗しました。 これは、NDIS のバグがある可能性があります。自体 SYS です。</p></td>
<td align="left"><p>この操作に失敗しました。 設定可能な値:</p>
<p>0x01 :NDIS_BUGCHECK_UNEXPECTED_FAILURE_KEWAITFORSINGLEOBJECT</p>
<p>Kewaitforsingleobject の 1 への呼び出しが失敗しました。</p></td>
<td align="left"><p>エラー状態コード</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x25</p></td>
<td align="left"><p>NDIS_BUGCHECK_WATCHDOG</p>
<p>ネットワーク スタックを管理しようとすると、時間がかかりすぎています。 NDIS は、他のドライバーに呼び出す、NDIS は呼び出しが迅速に完了したことを確認するウォッチドッグ タイマーを開始します。 呼び出し時間がかかりすぎる場合、NDIS はバグチェックを挿入します。</p>
<p>単純なデッドロックの可能性があります。 検索"! スタックの 2 つの ndis"または類似したにすべてのスレッド検索疑わしいかどうかを参照してください。 NDIS_WATCHDOG_TRIAGE_BLOCK、PrimaryThread に特別な注意してください。</p>
<p>可能性がありますが失われた NBLs、後者<strong><a href="-ndiskd-pendingnbls.md" data-raw-source="[!ndiskd.pendingnbls](-ndiskd-pendingnbls.md)">! ndiskd.pendingnbls</a></strong>役立つ場合があります。 チェックを使用して保持されている Oid を <strong><a href="-ndiskd-oid.md" data-raw-source="[!ndiskd.oid](-ndiskd-oid.md)">! ndiskd.oid</a></strong>します。</p></td>
<td align="left"><p>この操作は、時間がかかりすぎました。 設定可能な値:</p>
<ul>
<li><p>0x01 :NDIS_BUGCHECK_WATCHDOG_PROTOCOL_PAUSE</p>
<p>プロトコル ドライバーを一時停止中にタイムアウトが発生しました。</p></li>
<li><p>0x02 :NDIS_BUGCHECK_WATCHDOG_PROTOCOL_NETPNPEVENT</p>
<p>NET_PNP_EVENT_NOTIFICATION をプロトコル ドライバーに配信中にタイムアウトが発生しました。</p></li>
<li><p>0x03 :NDIS_BUGCHECK_WATCHDOG_PROTOCOL_STATUS_INDICATION</p>
<p>状態の表示をプロトコル ドライバーに配信中にタイムアウトが発生しました。</p></li>
<li><p>0x04 :NDIS_BUGCHECK_WATCHDOG_PROTOCOL_UNBIND</p>
<p>プロトコル ドライバーをバインド解除中にタイムアウトが発生しました。</p></li>
<li><p>パターン:NDIS_BUGCHECK_WATCHDOG_FILTER_PAUSE</p>
<p>フィルター ドライバーを一時停止中にタイムアウトが発生しました。</p></li>
<li><p>0x12:NDIS_BUGCHECK_WATCHDOG_FILTER_NETPNPEVENT</p>
<p>フィルター ドライバー、NET_PNP_EVENT_NOTIFICATION を配信中にタイムアウトが発生しました。</p></li>
<li><p>0x13:NDIS_BUGCHECK_WATCHDOG_FILTER_STATUS_INDICATION</p>
<p>フィルター ドライバーの状態を示す値を提供する一方、タイムアウトが発生しました。</p></li>
<li><p>0x14:NDIS_BUGCHECK_WATCHDOG_FILTER_DETACH</p>
<p>フィルター ドライバーのデタッチ中にタイムアウトが発生しました。</p></li>
<li><p>0x21:NDIS_BUGCHECK_WATCHDOG_MINIPORT_PAUSE</p>
<p>ミニポート アダプタを一時停止中にタイムアウトが発生しました。</p></li>
<li><p>0x22:NDIS_BUGCHECK_WATCHDOG_MINIPORT_HALT</p>
<p>ミニポート アダプターが停止中にタイムアウトが発生しました。</p></li>
<li><p>0x23:NDIS_BUGCHECK_WATCHDOG_MINIPORT_OID</p>
<p>ミニポート アダプターに、OID 要求を配信中にタイムアウトが発生しました。</p></li>
<li><p>0x24:NDIS_BUGCHECK_WATCHDOG_FILTER_OID</p>
<p>フィルター ドライバー、OID 要求を配信中にタイムアウトが発生しました。</p></li>
<li><p>0x25:NDIS_BUGCHECK_WATCHDOG_MINIPORT_IDLE</p>
<p>ミニポート アダプターをアイドル状態である中にタイムアウトが発生しました。</p></li>
<li><p>0x26:NDIS_BUGCHECK_WATCHDOG_CANCEL_IDLE</p>
<p>ミニポート アダプターをアイドル状態の要求のキャンセル中にタイムアウトが発生しました。</p></li>
</ul></td>
<td align="left"><p>Ndis にキャストされます。NDIS_WATCHDOG_TRIAGE_BLOCK します。 有用なフィールド:</p>
<ul>
<li><strong>StartTime</strong> KeQueryInterruptTime によって返される時間、操作の開始の 100 ナノ秒単位で示しています。</li>
<li><strong>TimeoutMilliseconds</strong>期間 NDIS、待機には、少なくともこのバグチェックをトリガーする前に示しています。</li>
<li><strong>TargetObject</strong>プロトコル、フィルター モジュール、またはで待機している NDIS ミニポート アダプターへのハンドルします。 実行 <strong><a href="-ndiskd-protocol.md" data-raw-source="[!ndiskd.protocol](-ndiskd-protocol.md)">! ndiskd.protocol</a></strong>、  <strong><a href="-ndiskd-filter.md" data-raw-source="[!ndiskd.filter](-ndiskd-filter.md)">! ndiskd.filter</a></strong>、または <strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd.netadapter</a></strong>詳細については、このハンドルを使用します。</li>
<li><strong>PrimaryThread</strong> NDIS が、操作を開始したスレッドです。 通常、操作が非同期的に処理される場合に、スレッドを他の場所で及ぼしてが可能性がありますが、検索するには、まずは、します。</li>
</ul></td>
<td align="left"><p>パラメーター 4 の値は、パラメーター 2 の値によって異なります。 この一覧の各番号は、パラメーター 2 で同じの 16 進数値に対応します。</p>
<ul>
<li>0x01 :0</li>
<li>0x02 :スタックのイベントの NET_PNP_EVENT_CODE します。 これらのコードの詳細については、次を参照してください <strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff568751" data-raw-source="[NET_PNP_EVENT](https://msdn.microsoft.com/library/windows/hardware/ff568751)">NET_PNP_EVENT</a></strong>.。</li>
<li>0x03 :スタックの表示の NDIS_STATUS コードです。 使用<strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">! ndiskd.help</a></strong>にデコードします。</li>
<li>0x04 :0</li>
<li>パターン:0</li>
<li>0x12:スタックのイベントの NET_PNP_EVENT_CODE します。 使用可能な値は、このリストのアイテム 2 の値の前の一覧を参照してください。</li>
<li>0x13:スタックの表示の NDIS_STATUS コードです。 使用<strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">! ndiskd.help</a></strong>にデコードします。</li>
<li>0x14:0</li>
<li>0x21:0</li>
<li>0x22:0</li>
<li>0x23:スタックの要求の OID コードです。 使用<strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">! ndiskd.help</a></strong>にデコードします。</li>
<li>0x24:スタックの要求の OID コードです。 使用<strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">! ndiskd.help</a></strong>にデコードします。</li>
<li>0x25:0</li>
<li>0x26:0</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p>0x26</p></td>
<td align="left"><p>NDIS_BUGCHECK_INVALID_OID_COMPLETION</p>
<p>ミニポート ドライバーが、現在保留中でない OID 要求を完了しようとしています。 そのミニポート ドライバーにします。 1 つ以上の時間は同じ要求を完了しようとしています。 ドライバーの可能性があります。</p></td>
<td align="left"><p>バグチェックの原因となったミニポート ドライバーのハンドル。 実行<strong><a href="-ndiskd-minidriver.md" data-raw-source="[!ndiskd.minidriver](-ndiskd-minidriver.md)">! ndiskd.minidriver</a></strong>詳細については、このハンドルを使用します。</p></td>
<td align="left"><p>NDIS OID 要求ミニポート ドライバーが完了しようとしています。 実行しようとしてできます<strong><a href="-ndiskd-oid.md" data-raw-source="[!ndiskd.oid](-ndiskd-oid.md)">! ndiskd.oid</a></strong>この要求が、メモリが有効でないこの時点でします。</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x27</p></td>
<td align="left"><p>NDIS_BUGCHECK_LEAKED_NBL</p>
<p>ドライバーが漏洩した、 <strong><a href="https://msdn.microsoft.com/library/windows/hardware/ff568388" data-raw-source="[NET_BUFFER_LIST](https://msdn.microsoft.com/library/windows/hardware/ff568388)">NET_BUFFER_LIST</a></strong>構造体。 確認<strong><a href="-ndiskd-pendingnbls.md" data-raw-source="[!ndiskd.pendingnbls](-ndiskd-pendingnbls.md)">! ndiskd.pendingnbls</a></strong>任意 NBLs を表示するこのドライバーで保留中のあります。</p></td>
<td align="left"><p>場所、リークが検出されました。 設定可能な値:</p>
<ul>
<li><p>0x01 :NBL の追跡ツールでメモリ リークが検出されました。 現在の登録を解除またはバインド解除されているドライバーでは、最も一般的な原因です。 バグチェック スレッドの呼び出し履歴を確認します。 ドライバーは、バインド解除またはこれらの鉄則 active NBLs 中の登録を解除する必要がありますできません。</p></li>
</ul></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

パラメーター 1 が、BUGCODE の具体的な原因を示す\_NDIS\_ドライバーのバグ チェックします。

<a name="remarks"></a>コメント
-------

BUGCODE\_NDIS\_ネットワーク ドライバーのドライバーのバグチェック indendifies 問題。 多くの場合、問題は、NDIS ミニポート ドライバーで発生します。 使用して、NDIS ミニポート ドライバーの完全な一覧を取得する[ **! ndiskd.netadapter**](-ndiskd-netadapter.md)します。 ネットワーク スタックとの大きな画像概要を取得できます[ **! ndiskd.netreport**](-ndiskd-netreport.md)します。

このバグ チェック コードは、Microsoft Windows Server 2003 と Windows の以降のバージョンでのみ発生します。 Windows 2000、Windows XP では、対応するコード[**バグ チェック 0xD2** ](bug-check-0xd2--bugcode-id-driver.md) (BUGCODE\_ID\_ドライバー)。

 

 




