---
title: モニターのホット プラグ検出
description: モニターのホット プラグ検出
ms.assetid: 170d2d5d-fd46-431d-9672-61fa048f7dd2
keywords:
- ビデオの WDK 表示のネットワークを表示、ホットプラグ検出
- VidPN WDK の表示、ホット プラグの検出
- WDK 存在するネットワークのビデオのビデオ出力コネクタ
- HPD 認識 WDK ビデオ存在するネットワーク
- ホット検出 WDK ビデオ存在するネットワークを接続します。
- 接続されていない検出 WDK ビデオ存在するネットワーク
- WDK ビデオ存在するネットワークの接続モニター
- WDK ビデオ存在するネットワーク モニターを接続していません。
- 接続されていないモニター WDK ビデオ存在するネットワーク
- ポータブル コンピューターのビデオ出力 WDK ビデオ存在するネットワーク
- モバイル コンピューターのビデオ出力 WDK ビデオ存在するネットワーク
- ホットなモニター検出 WDK ビデオ存在するネットワークを接続します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67fa574b01164ef151feb6823eb66068f1749eb0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323708"
---
# <a name="monitor-hot-plug-detection"></a>モニターのホット プラグ検出


ディスプレイ アダプターのビデオの出力は、子のデバイスのディスプレイ アダプターと見なされます。 モニターまたはその他の出力に接続する外付けディスプレイ デバイスには、子デバイスはありません。 初期化中に、ディスプレイのミニポート ドライバーの[ **DxgkDdiQueryChildRelations** ](https://msdn.microsoft.com/library/windows/hardware/ff559750)型と HPD 認識値関数はそれぞれの子デバイスを割り当てます。 種類は、のいずれか、 [ **DXGK\_子\_デバイス\_型**](https://msdn.microsoft.com/library/windows/hardware/ff561008)列挙子。

-   **TypeVideoOutput**

-   **TypeOther**

HPD 認識値が 1 の[ **DXGK\_子\_デバイス\_HPD\_認識**](https://msdn.microsoft.com/library/windows/hardware/ff561006)列挙子。

-   **HpdAwarenessAlwaysConnected**

-   **HpdAwarenessInterruptible**

-   **HpdAwarenessPolled**

型を持つ子デバイス**TypeVideoOutput** HPD 認識値以外の**HpdAwarenessAlwaysConnected**と呼ばれますが、*ビデオ出力コネクタ*。

ドライバーが HPD 認識値設定して、割り込み可能なデバイスの動作をエミュレートする必要がありますディスプレイのミニポート ドライバーでは、ビデオの出力に、モニターが接続されているかどうかを判断できない場合、 **HpdAwarenessInterruptible**します。 ディスプレイのミニポート ドライバーは、テレビのビューに切り替えるにキーボード ショートカットを入力すると、ドライバーで呼び出す必要がありますなど、割り込み可能なモニターがビデオの出力に接続することを示す必要がある場合、 [ **DxgkCbIndicateChildStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff559522)関数と*ChildStatus*.**ホットプラグ**.**接続されている**設定**TRUE**します。

オペレーティング システムがディスプレイのミニポート ドライバーがの HPD 認識の値を持つすべてのビデオ出力コネクタの状態を報告することを要求、特定の時間に**HpdAwarenessPolled**します。 通常のポーリング間隔はありません。代わりに、要求は、特定デバイスの使用可能な表示モードの一覧を更新する必要があるときに行われます。 たとえば、ラップトップ コンピューターがドッキングされているときに、オペレーティング システムをドッキング ステーションのビデオ出力に、モニターが接続されているかどうかを把握する必要があります。 オペレーティング システムでは、ディスプレイのミニポート ドライバーを呼び出すことによって、要求を[ **DxgkDdiQueryChildStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff559754)の HPD 認識値を持つ子デバイスごとに関数**HpdAwarenessPolled**します。

HPD 認識の値を持つビデオ出力のコネクタに対して**HpdAwarenessInterruptible**ディスプレイのミニポート ドライバーは、外付けディスプレイ デバイスが接続されているホットたびに、オペレーティング システムに通知するため、または電源が入っていません。 ディスプレイ ミニポート ドライバーの割り込み処理コードの呼び出し、ディスプレイ ポート ドライバーの[ **DxgkCbIndicateChildStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff559522)外付けディスプレイ デバイスに接続されているレポートに関数または特定のビデオ出力から切断されます。 ラップトップ コンピューターがドッキングされているとき、ディスプレイのミニポート ドライバーの[ *DxgkDdiNotifyAcpiEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff559695)関数を呼び出す必要があります**DxgkCbIndicateChildStatus**で各ビデオの出力ドッキング ステーションの HPD 認識値を持つ**HpdAwarenessInterruptible**します。

場合の HPD 認識値を持つコネクタ**HpdAwarenessPolled**が使用不能な (つまりカバー) ラップトップ コンピューターがドッキングされているとき、ディスプレイのミニポート ドライバーの*DxgkDdiNotifyAcpiEvent*関数を呼び出す必要があります**DxgkCbIndicateChildStatus**コネクタが切断されていることを報告します。

ポータブル コンピューターで、統合表示パネルに関連付けられているビデオの出力は、特殊なケースです。 ポータブル コンピューターのカバーするかどうかを把握するオペレーティング システムのニーズが開くか、終了する場合に、そのためのアイデア*接続されている*オープンとのことを意味するために使用*接続されていない*ことを意味するために使用終了します。 ポータブル コンピューターで、統合されたディスプレイに関連付けられているビデオ出力がの HPD 認識値**HpdAwarenessInterruptible**します。 わけ、ただし、カバーを開くまたは閉じるときにディスプレイ アダプターが割り込みを生成します。 代わりに、ACPI BIOS では、カバーを開くまたは閉じるときに、割り込みが生成されます。 ディスプレイのミニポート ドライバーの呼び出しで結果を中断する[ *DxgkDdiNotifyAcpiEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff559695)を呼び出す関数**DxgkCbIndicateChildStatus**状態を報告するには(オープンまたはクローズ) のカバーします。 ディスプレイのミニポート ドライバーでは、カバーのステータスをレポートを設定して、 **HotPlug.Connected**のメンバー、 [ **DXGK\_子\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff561010)構造体を**TRUE** (開く) または**FALSE** (終了) を渡して、DXGK\_子\_状態構造体を**DxgkCbIndicateChildStatus**.

次の一覧は、モニターがコネクタに HPD 認識価値があると仮定すると、HD15 コネクタに接続されているときの手順を説明します。 **HpdAwarenessPolled**します。

1.  モニターは、ディスプレイ アダプターの HD15 コネクタに接続されます。 ディスプレイ アダプターを検出しませんこのホットプラグ イベントとして。

2.  いくつかの将来の時点では、ユーザー モード アプリケーションは、ディスプレイ デバイスの一覧を要求します。

3.  HPD 認識値を持つディスプレイ アダプターの場合は、各ビデオ出力コネクターの**HpdAwarenessPolled**、VidPN マネージャーには、ディスプレイのミニポート ドライバーの[ **DxgkDdiQueryChildStatus**](https://msdn.microsoft.com/library/windows/hardware/ff559754)外付けディスプレイ デバイスが接続されているかどうかを判断する関数。 ときに*DxgkDdiQueryChildStatus*呼びます HD15 コネクタは外部の監視が実際に接続されていることを報告します。

次の一覧は、モニターがコネクタに HPD 認識価値があると仮定した場合、DVI コネクタに接続しているときの後に手順を説明します。 **HpdAwarenessInterruptible**します。

1.  フラット パネルは、ディスプレイ アダプターの DVI コネクタに接続されます。

2.  ディスプレイ アダプターでは、ホット プラグ イベントを検出し、割り込みを生成します。

3.  ディスプレイ ミニポート ドライバーの割り込みが処理される[ **DxgkDdiInterruptRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff559680)関数で、遅延プロシージャ呼び出し (DPC) のスケジュールを設定します。 その後表示ミニポート ドライバーの DPC のコールバック関数が呼び出されます。

4.  DPC のコールバック関数に渡します、DXGK\_子\_ディスプレイ ポート ドライバーの状態の構造体[ **DxgkCbIndicateChildStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff559522) DVI の状態を報告する関数コネクタです。 **ChildUid** 、DXGK のメンバー\_子\_ステータス構造体、DVI コネクタの識別と**HotPlug.Connected**メンバー (に設定**TRUE**ここでは)、外付けディスプレイ デバイスが接続されていることを示します。

DVI コネクタを 3 つの分岐を持つドングルをサポートするいるとします。DVI、HD15、および s-ビデオ。 その場合は、ディスプレイのミニポート ドライバーは、1 つの物理 DVI コネクタに関連付けられている 3 つの子デバイスを以前列挙は。DVI-DVI 上、DVI で HD15、および S DVI ビデオで。 これらの各子デバイスの種類になります**TypeVideoOutput**および HPD 認識値**HpdAwarenessInterruptible**します。 次の一覧には、モニターがドングルの HD15 分岐に接続しているときの手順について説明します。

1.  ディスプレイ アダプターでは、ホット プラグ イベントを検出し、割り込みを生成します。

2.  ディスプレイ ミニポート ドライバーの割り込みが処理される[ **DxgkDdiInterruptRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff559680)関数で、遅延プロシージャ呼び出し (DPC) のスケジュールを設定します。 その後表示ミニポート ドライバーの DPC のコールバック関数が呼び出されます。

3.  DPC のコールバック関数では、ホット プラグ イベントがドングル (HD15 で DVI) の HD15 分岐ことが判断されます。

4.  DPC のコールバック関数に渡します、DXGK\_子\_状態構造体を[ **DxgkCbIndicateChildStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff559522) HD15-DVI にビデオ出力のステータスを報告します。 **ChildUid** 、DXGK のメンバー\_子\_ステータス構造体は、ビデオの出力を識別し、 **HotPlug.Connected**メンバー (に設定**TRUE**ここでは)、外付けディスプレイ デバイスが接続されていることを示します。

次の一覧には、ラップトップ コンピューターのカバーを閉じたときの手順について説明します。

1.  ACPI イベントが生成されますが、ポータブル コンピューターのカバーを閉じた。 その後、ディスプレイ ミニポート ドライバーの[ *DxgkDdiNotifyAcpiEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff559695)関数が呼び出されます。

2.  *DxgkDdiNotifyAcpiEvent*渡します、DXGK\_子\_ディスプレイ ポート ドライバーの状態の構造体**DxgkCbIndicateChildStatus**関連付けられている子デバイスの状態を報告する関数組み込みのパネルを表示します。 具体的には、 *DxgkDdiNotifyAcpiEvent*設定、 **HotPlug.Connected** 、DXGK のメンバー\_子\_状態構造体を**FALSE**します。

 

 





