---
title: ブート ドライブを管理するミニポート ドライバーに関する制約
description: ブート ドライブを管理するミニポート ドライバーに関する制約
ms.assetid: 78375e9b-8be9-4e64-b90e-cc8c4ab1751b
keywords:
- ストレージ ミニポート ドライバー WDK、ブート ドライブ
- ミニポート ドライバー WDK ストレージ、ブート ドライブ
- ブート ドライブの WDK ストレージ
- ディスク ダンプ ドライバー WDK ストレージ
- ダンプ モード WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8054aab82bd62b7a47b8d6b3025effaad30d31b2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346542"
---
# <a name="restrictions-on-miniport-drivers-that-manage-the-boot-drive"></a>ブート ドライブを管理するミニポート ドライバーに関する制約


システムのクラッシュ時に特別な制限は、記憶域ミニポート ドライバーをブート デバイス用のアダプターを管理します。 ディスクにシステム メモリのイメージをダンプするには、中には、ミニポート ドライバーは、別の環境内で動作する必要があります。 ミニポート ドライバー、ポートのドライバーとディスク クラス ドライバー間の通常の通信が中断されました。 ディスク ダンプのポート ドライバーへの直接呼び出しによって、カーネルはディスク I/O *diskdump.sys* (*dumpata.sys* ATA コント ローラー)、ファイル システム、および通常の I/O スタックをバイパスします。 ディスク ダンプ ドライバーが、さらに、すべての I/O 操作を処理するために、ブート デバイスのミニポート ドライバーを呼び出すし、ディスク ダンプ ドライバーはすべてのポート ドライバーに、ミニポート ドライバーの呼び出しをインターセプトします。

ディスクのダンプ ドライバーは、ミニポート ドライバーがポート ルーチンを使用する同じ方法でディスク ダンプ ドライバー ルーチンを使用できるように、同じポート ドライバーが提供するサポート ルーチンのセットを提供します。

ただし、管理ディスク ダンプ パス内のアダプターのミニポート ドライバーは、ダンプのモードでは、次の制限が適用されます。

### <a name="span-idmemusagespanspan-idmemusagespanmemory-usage"></a><span id="mem_usage"></span><span id="MEM_USAGE"></span>メモリ使用量

ミニポート ドライバーでは、システムのクラッシュ時にメモリの消費が少ない使用を行う必要があります。 ミニポート ドライバーがそのデバイスとドライバーの拡張機能に割り当てることがキャッシュされていないメモリの量は、非常に制限されています。 ミニポート ドライバーが 32 キロバイト以上のメモリを割り当てるしないようにします。

### <a name="span-idaccessibilityspanspan-idaccessibilityspanaccessibility-of-the-boot-device"></a><span id="accessibility"></span><span id="ACCESSIBILITY"></span>ブート デバイスのユーザー補助機能

ミニポートが初期化ルーチンから戻る前に、ブート デバイスがアクセスできる必要があります ([**HwStorInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff557396) StorPort のおよび[ *HwScsiInitialize* ](https://msdn.microsoft.com/library/windows/hardware/ff557302) SCSI ポート)。 オペレーティング システムは、初期化ルーチンが完了したら、任意の時点で、ブート デバイスにコマンドを送信可能性があります。

### <a name="span-idbusresetsspanspan-idbusresetsspanbus-resets"></a><span id="bus_resets"></span><span id="BUS_RESETS"></span>バスのリセット

ミニポート ドライバー、バスのリセットへの要求を無視する必要があります ([**HwStorResetBus** ](https://msdn.microsoft.com/library/windows/hardware/ff557415) StorPort のおよび[ *HwScsiResetBus* ](https://msdn.microsoft.com/library/windows/hardware/ff557318) scsiポート)。

### <a name="span-iddpcsspanspan-iddpcsspandeferred-procedure-calls-dpcs"></a><span id="dpcs"></span><span id="DPCS"></span>遅延プロシージャ呼び出し (Dpc)

StorPort ミニポート ドライバー DPC ルーチンを初期化するために読み取ろうとしないで ([**HwStorDpcRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff557383)) と[ **StorPortInitializeDpc**](https://msdn.microsoft.com/library/windows/hardware/ff567110)します。 通常、処理は、割り込み要求中に、DPC ルーチンを実行する必要があります、その要求のコンテキストで発生するこの場合、キューに置かれました。

### <a name="span-idmultiplerequestsspanspan-idmultiplerequestsspanmultiple-requests-per-logical-unit"></a><span id="multiple_requests"></span><span id="MULTIPLE_REQUESTS"></span>論理ユニットごとの複数の要求

ディスク ダンプ ポート ドライバーでは、論理ユニットごとの複数の要求を送信しません。 そのため、どのような値のミニポート ドライバーに割り当てます関係ありません、 **MultipleRequestPerLu**のメンバー [**ポート\_構成\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff563901).

### <a name="span-idpollingspanspan-idpollingspanpolling-and-time-checking"></a><span id="polling"></span><span id="POLLING"></span>ポーリングと時のチェック

ミニポート ドライバーなどのルーチンをチェックする時間に依存しない[ **ScsiPortQuerySystemTime** ](https://msdn.microsoft.com/library/windows/hardware/ff564708)または[ **StorPortQuerySystemTime** ](https://msdn.microsoft.com/library/windows/hardware/ff567465)ダンプのモードで実行中には ミニポート ドライバーのベスト プラクティスは除外を使用して、 [ **KeQuerySystemTime** ](https://msdn.microsoft.com/library/windows/hardware/ff553068)ルーチンをいつでも、ミニポート ドライバーはする必要があります常にポート ドライバー ライブラリのルーチンを使用して時刻を確認するためです。

### <a name="span-idirqlspanspan-idirqlspaninterrupt-request-level"></a><span id="irql"></span><span id="IRQL"></span>割り込み要求レベル

ランタイム ポート ドライバー [ **HwStorFindAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff557390)と[ *HwScsiFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff557300)パッシブ IRQL でします。 ただし、ダンプ ドライバーは、パッシブより大きい IRQL ですべてのミニポート ルーチンを呼び出します。 そのため、ダンプ パスのミニポート ドライバーでは、パッシブ IRQL で実行する必要がありますレジストリ アクセスなどの操作を回避する必要があります。

### <a name="span-idtargetandlunspanspan-idtargetandlunspantarget-ids-and-logical-unit-numbers-luns"></a><span id="target_and_lun"></span><span id="TARGET_AND_LUN"></span>ターゲット Id および論理ユニット番号 (Lun)

ミニポート ドライバーする必要がありますいないを使用して、別のターゲットの ID と LUN ブート デバイスのダンプ プロセス中に。

ブートまたはダンプのパスでの記憶域ミニポート ドライバーでは、ダンプのモードで実行されているかどうかを検出する必要があります。 オペレーティング システムは、ミニポート ドライバーがダンプ モードで実行中またはオペレーティング システムが休止状態に変更する記憶域ミニポート ドライバーを通知する 2 つの方法はあります。

-   オペレーティング システムに渡します**NULL**ミニポート ドライバーの引数*DriverEntry*ルーチン。

-   ディスク ダンプ ポート ドライバーには文字列の"ダンプ = 1"で、*引き*パラメーターを呼び出すときに、 [ **HwStorFindAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff557390)または[ *HwScsiFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff557300)ルーチン。

ドライバー名のプレフィックスになりますダンプ モードでの記憶域ミニポート ドライバーのイメージのデバッガーで確認すると"ダンプ\_"。 ドライバー名のプレフィックスには、ミニポート ドライバーが休止状態モードの場合は、"休止\_"。

 

 




