---
title: ホットプラグ検出の監視
description: ホットプラグ検出の監視
ms.assetid: 170d2d5d-fd46-431d-9672-61fa048f7dd2
keywords:
- ビデオの現在のネットワーク WDK ディスプレイ、ホットプラグ検出
- VidPN WDK ディスプレイ、ホットプラグ検出
- ビデオ出力コネクタ WDK ビデオの現在のネットワーク
- HPD 認識用 WDK ビデオの現在のネットワーク
- ホットプラグ検出 WDK ビデオの現在のネットワーク
- 検出を切断した WDK ビデオの現在のネットワーク
- 接続モニター WDK ビデオの現在のネットワーク
- 接続されていない監視 WDK ビデオの現在のネットワーク
- 未接続の監視 WDK ビデオの現在のネットワーク
- ポータブルコンピューターのビデオ出力 WDK ビデオの現在のネットワーク
- モバイルコンピューターのビデオ出力 WDK ビデオの現在のネットワーク
- ホットプラグ検出 WDK ビデオの現在のネットワークを監視する
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbfee78fb3f00814680280b773fbf868df8f2b2f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840554"
---
# <a name="monitor-hot-plug-detection"></a>ホットプラグ検出の監視


ディスプレイアダプターのビデオ出力は、ディスプレイアダプターの子デバイスと見なされます。 出力に接続するモニターまたはその他の外付けディスプレイデバイスは、子デバイスとは見なされません。 初期化中に、ディスプレイミニポートドライバーの[**DxgkDdiQueryChildRelations**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_child_relations)関数は、各子デバイスに種類と hpd 認識値を割り当てます。 この型は、[**デバイス\_型列挙子の DXGK\_子\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ne-dispmprt-_dxgk_child_device_type)の1つです。

-   **TypeVideoOutput**

-   **TypeOther**

HPD 認識値は、 [**DXGK\_子\_デバイス\_hpd\_認識**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_dxgk_child_device_hpd_awareness)列挙子の1つです。

-   **HpdAwarenessAlwaysConnected**

-   **HpdAwarenessInterruptible**

-   **HpdAwarenessPolled**

種類が**TypeVideoOutput**で、 **HpdAwarenessAlwaysConnected**以外の hpd 認識値を持つ子デバイスは、"*ビデオ出力コネクタ*" と呼ばれます。

モニタがビデオ出力に接続されているかどうかを表示ミニポートドライバーが判断できない場合、ドライバーは、HPD 認識値を**HpdAwarenessInterruptible**に設定して、割り込み可能なデバイスの動作をエミュレートする必要があります。 表示ミニポートドライバーで、割り込み可能なモニターがビデオ出力に接続されていることを示す必要がある場合 (ユーザーがテレビ表示に切り替えるためにキーボードショートカットを入力したときなど)、ドライバーは[**DxgkCbIndicateChildStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_indicate_child_status)を呼び出す必要があります。*Childstatus*の関数。**HotPlug**。Connected が**TRUE**に設定**されて**います。

オペレーティングシステムは、特定のタイミングで、HPD 認識値が**HpdAwarenessPolled**のすべてのビデオ出力コネクタの状態を、表示ミニポートドライバーに報告するように要求します。 定期的なポーリング間隔がありません。代わりに、使用可能なディスプレイデバイスとモードの一覧を更新する必要がある場合に、要求が行われます。 たとえば、ラップトップコンピューターがドッキングされている場合、オペレーティングシステムは、モニターがドッキングステーションのビデオ出力に接続されているかどうかを確認する必要があります。 オペレーティングシステムは、HPD 認識値が**HpdAwarenessPolled**の各子デバイスに対して、ディスプレイミニポートドライバーの[**DxgkDdiQueryChildStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_child_status)関数を呼び出すことによって、要求を行います。

HPD 認識値が**HpdAwarenessInterruptible**のビデオ出力コネクタの場合、ディスプレイミニポートドライバーは、外部ディスプレイデバイスがホットプラグまたは取り外されたときに、オペレーティングシステムに通知します。 ディスプレイミニポートドライバーの割り込み処理コードは、ディスプレイポートドライバーの[**DxgkCbIndicateChildStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_indicate_child_status)関数を呼び出して、外部ディスプレイデバイスが特定のビデオ出力に接続されているか切断されたことを報告します。 ラップトップコンピューターがドッキングされている場合、ディスプレイミニポートドライバーの[*DxgkDdiNotifyAcpiEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event)関数は、hpd 認識の **値がであるドッキングステーション上の各ビデオ出力に対して DxgkCbIndicateChildStatus を呼び出す必要があります。HpdAwarenessInterruptible**。

ラップトップコンピューターがドッキングされているときに、HPD 認識値が**HpdAwarenessPolled**のコネクタが使用不能になった場合 (つまり、表示されている場合)、ミニポートドライバーの*DxgkDdiNotifyAcpiEvent*関数はを呼び出す**必要があります。DxgkCbIndicateChildStatus**は、コネクタが切断されたことを報告します。

ポータブルコンピューター上の統合された表示パネルに関連付けられているビデオ出力は、通常とは異なる場合があります。 オペレーティングシステムは、ポータブルコンピューターのカバーが開いているか閉じられているかどうかを知る必要があるため、*接続*されて*いない*という考え方を使用して、閉じたことを意味します。 ポータブルコンピューター上の統合ディスプレイに関連付けられているビデオ出力には、HPD 認識値**HpdAwarenessInterruptible**があります。 しかし、lid が開いたり閉じられたりしたときに、ディスプレイアダプターによって割り込みが生成されるわけではありません。 代わりに、ふたが開いたり閉じられたりしたときに、ACPI BIOS によって割り込みが生成されます。 この割り込みにより、ディスプレイミニポートドライバーの[*DxgkDdiNotifyAcpiEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event)関数が呼び出されます。この関数は、 **DxgkCbIndicateChildStatus**を呼び出して、カバーの状態 (オープンまたはクローズ) を報告します。 ディスプレイミニポートドライバーは、 [**DXGK\_子\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_child_status)構造の**HotPlug**メンバーを**TRUE** (open) または**FALSE** (CLOSED) に設定し、DXGK\_子を渡すことによって、カバーの状態を報告し @no**DxgkCbIndicateChildStatus**の状態構造体に変換します。\_

次の一覧では、コネクタが**HpdAwarenessPolled**の hpd 認識値を持つことを前提として、HD15 コネクタにモニターが接続されている場合の手順について説明します。

1.  モニターは、ディスプレイアダプターの HD15 コネクタに接続されています。 ディスプレイアダプターでは、これはホットプラグイベントとして検出されません。

2.  将来、ユーザーモードアプリケーションがディスプレイデバイスの一覧を要求します。

3.  HPD 認識値が**HpdAwarenessPolled**であるディスプレイアダプターの各ビデオ出力コネクタについて、VidPN マネージャーはディスプレイミニポートドライバーの[**DxgkDdiQueryChildStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_child_status)関数を呼び出して、外部ディスプレイかどうかを判断します。デバイスが接続されています。 HD15 コネクタに対して*DxgkDdiQueryChildStatus*が呼び出されると、外部モニターが実際に接続されていることを報告します。

次の一覧では、コネクタに HPD 認識値**HpdAwarenessInterruptible**があると仮定して、モニターが DVI コネクタに接続されている場合の手順について説明します。

1.  フラットパネルは、ディスプレイアダプターの DVI コネクタに接続されています。

2.  ディスプレイアダプターは、ホットプラグイベントを検出し、割り込みを生成します。

3.  割り込みは、ディスプレイミニポートドライバーの[**DxgkDdiInterruptRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_interrupt_routine)関数によって処理されます。この関数は、遅延プロシージャ呼び出し (DPC) をスケジュールします。 その後、ディスプレイミニポートドライバーの DPC コールバック関数が呼び出されます。

4.  DPC コールバック関数は、DXGK\_CHILD\_STATUS 構造体をディスプレイポートドライバーの[**DxgkCbIndicateChildStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_indicate_child_status)関数に渡して、DVI コネクタの状態を報告します。 DXGK\_CHILD\_STATUS 構造体の**ChildUid**メンバーは、DVI コネクタを識別し、 **HotPlug**メンバー (この場合は**TRUE**に設定されます) は、外部ディスプレイデバイスが接続されていることを示します。

Dvi コネクタで、DVI、HD15、S-video という3つの分岐があるドングルがサポートされているとします。 この場合、ディスプレイミニポートドライバーは、1つの物理 DVI コネクタに関連付けられた3つの子デバイス (DVI、HD15、および S-video) を既に列挙しています。 これらの各子デバイスは、 **TypeVideoOutput**の種類と**HpdAwarenessInterruptible**の hpd 認識値を持ちます。 次の一覧では、モニターがドングルの HD15 ブランチに接続されている場合の手順について説明します。

1.  ディスプレイアダプターは、ホットプラグイベントを検出し、割り込みを生成します。

2.  割り込みは、ディスプレイミニポートドライバーの[**DxgkDdiInterruptRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_interrupt_routine)関数によって処理されます。この関数は、遅延プロシージャ呼び出し (DPC) をスケジュールします。 その後、ディスプレイミニポートドライバーの DPC コールバック関数が呼び出されます。

3.  DPC コールバック関数は、ホットプラグイベントがドングルの HD15 ブランチ (HD15) 上にあったかどうかを判断します。

4.  DPC コールバック関数は、DXGK\_子\_状態構造体を[**DxgkCbIndicateChildStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_indicate_child_status)に渡して、HD15 ビデオ出力の状態を報告します。 DXGK\_子\_STATUS 構造体の**ChildUid**メンバーはビデオ出力を識別し、 **HotPlug**メンバー (この場合は**TRUE**に設定されます) は、外部ディスプレイデバイスが接続されていることを示します。

次の一覧では、ラップトップコンピューターでカバーが閉じられたときの手順について説明します。

1.  カバーは、ACPI イベントを生成するポータブルコンピューターで閉じられます。 その後、ディスプレイミニポートドライバーの[*DxgkDdiNotifyAcpiEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_notify_acpi_event)関数が呼び出されます。

2.  *DxgkDdiNotifyAcpiEvent*は、組み込みの表示パネルに関連付けられている子デバイスの状態を報告するために、DXGK\_CHILD\_status 構造体を表示ポートドライバーの**DxgkCbIndicateChildStatus**関数に渡します。 具体的には、 *DxgkDdiNotifyAcpiEvent*は、DXGK\_子\_STATUS 構造体の**HotPlug**メンバーを**FALSE**に設定します。

 

 





