---
title: ブート ドライブを管理するミニポート ドライバーに関する制約
description: ブート ドライブを管理するミニポート ドライバーに関する制約
ms.assetid: 78375e9b-8be9-4e64-b90e-cc8c4ab1751b
keywords:
- 記憶域ミニポートドライバー WDK、ブートドライブ
- ミニポートドライバー WDK 記憶域、ブートドライブ
- ブートドライブ WDK 記憶域
- ディスクダンプドライバー WDK ストレージ
- ダンプモード WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70dce1a215b45e684beeeb1a68597a1d86b92118
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842692"
---
# <a name="restrictions-on-miniport-drivers-that-manage-the-boot-drive"></a>ブート ドライブを管理するミニポート ドライバーに関する制約


ブートデバイス用のアダプターを管理する記憶域ミニポートドライバーは、システムのクラッシュ時に特別な制限を受けることがあります。 システムのメモリイメージをディスクにダンプするときに、ミニポートドライバーを別の環境で動作させる必要があります。 ミニポートドライバー、ポートドライバー、およびディスククラスドライバー間の通常の通信は中断されます。 カーネルでは、ディスクダンプポートドライバー、 *diskdump .sys* (ATA コントローラーの*dumpata* )、ファイルシステムのバイパス、および通常の i/o スタックを直接呼び出すことによって、ディスク i/o が行われます。 その後、ディスクダンプドライバーは、すべての i/o 操作を処理するためにブートデバイスのミニポートドライバーを呼び出します。また、ディスクダンプドライバーは、ポートドライバーへのすべてのミニポートドライバーの呼び出しをインターセプトします。

ディスクダンプドライバーは、ポートドライバーが提供するものと同じサポートルーチンのセットを提供します。そのため、ミニポートドライバーは、ポートルーチンを使用する場合と同じ方法で、ディスクダンプドライバールーチンを使用できるようにする必要があります。

ただし、ディスクダンプパスでアダプターを管理するミニポートドライバーでは、ダンプモードでは次の制限が適用されます。

### <a name="span-idmem_usagespanspan-idmem_usagespanmemory-usage"></a><span id="mem_usage"></span><span id="MEM_USAGE"></span>メモリ使用量

ミニポートドライバーは、システムのクラッシュ中にメモリを高速に使用する必要があります。 ミニポートドライバーがデバイスとドライバーの拡張機能に割り当てることができる、キャッシュされていないメモリの量は非常に限られています。 ミニポートドライバーは、32 kb を超えるメモリを割り当てないようにする必要があります。

### <a name="span-idaccessibilityspanspan-idaccessibilityspanaccessibility-of-the-boot-device"></a><span id="accessibility"></span><span id="ACCESSIBILITY"></span>ブートデバイスのユーザー補助

ブートデバイスは、ミニポートが初期化ルーチンから戻る前にアクセス可能である必要があります ([**HwStorInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_initialize)の場合は HWSCSIINITIALIZE、SCSI ポートの場合は[](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557302(v=vs.85)) )。 オペレーティングシステムは、初期化ルーチンが完了した後、いつでもブートデバイスにコマンドを送信することがあります。

### <a name="span-idbus_resetsspanspan-idbus_resetsspanbus-resets"></a><span id="bus_resets"></span><span id="BUS_RESETS"></span>バスのリセット

ミニポートドライバーは、バスをリセットするための要求を無視する必要があります (StorPort の場合は[**HwStorResetBus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_reset_bus) 、SCSI ポートの場合は[*HwScsiResetBus*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557318(v=vs.85)) )。

### <a name="span-iddpcsspanspan-iddpcsspandeferred-procedure-calls-dpcs"></a><span id="dpcs"></span><span id="DPCS"></span>遅延プロシージャ呼び出し (Dpc)

StorPort ミニポートドライバーは、 [**Storportinitializer Edpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportinitializedpc)を使用して DPC ルーチン ([**HwStorDpcRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_dpc_routine)) を初期化しようとすることはできません。 割り込み要求中に、DPC ルーチンへの実行のために通常キューに登録されている処理は、その要求のコンテキストで発生する必要があります。

### <a name="span-idmultiple_requestsspanspan-idmultiple_requestsspanmultiple-requests-per-logical-unit"></a><span id="multiple_requests"></span><span id="MULTIPLE_REQUESTS"></span>論理ユニットあたり複数の要求

ディスクダンプポートドライバーは、論理ユニットごとに複数の要求を送信しません。 そのため、[**ポート\_構成\_情報**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))の**MultipleRequestPerLu**メンバーにミニポートドライバーが割り当てる値は関係ありません。

### <a name="span-idpollingspanspan-idpollingspanpolling-and-time-checking"></a><span id="polling"></span><span id="POLLING"></span>ポーリングと時間チェック

ミニポートドライバーは、ダンプモードで実行中の[**ScsiPortQuerySystemTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportquerysystemtime)や[**Storportquerysystemtime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportquerysystemtime)などの時間チェックルーチンに依存しないようにする必要があります。 ミニポートドライバーでは、常に[**Kequerysystemtime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kequerysystemtime)ルーチンを使用しないことをお勧めします。ミニポートドライバーでは、常にポートドライバーライブラリルーチンを使用して時刻を確認する必要があるためです。

### <a name="span-idirqlspanspan-idirqlspaninterrupt-request-level"></a><span id="irql"></span><span id="IRQL"></span>割り込み要求レベル

ランタイムポートドライバーは、パッシブ IRQL で[**HwStorFindAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)と[*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))を呼び出します。 ただし、ダンプドライバーは、パッシブより高い IRQL ですべてのミニポートルーチンを呼び出します。 そのため、ダンプパスのミニポートドライバーは、パッシブ IRQL で実行する必要があるレジストリアクセスなどの操作を回避する必要があります。

### <a name="span-idtarget_and_lunspanspan-idtarget_and_lunspantarget-ids-and-logical-unit-numbers-luns"></a><span id="target_and_lun"></span><span id="TARGET_AND_LUN"></span>ターゲット Id と論理ユニット番号 (Lun)

ミニポートドライバーは、ダンプ処理中に、ブートデバイスに異なるターゲット ID と LUN を使用することはできません。

ブートパスまたはダンプパス内の記憶域ミニポートドライバーは、ダンプモードで実行されているかどうかを検出する必要があります。 オペレーティングシステムは、ミニポートドライバーがダンプモードで実行されているか、オペレーティングシステムが休止状態に変更されていることを、記憶域ミニポートドライバーに通知する2つの方法があります。

-   オペレーティングシステムが、ミニポートドライバーの*Driverentry*ルーチンに**NULL**引数を渡しています。

-   ディスクダンプポートドライバーは、 [**HwStorFindAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)または[*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))ルーチンを呼び出すときに、 *argumentstring*パラメーターに "dump = 1" という文字列を渡します。

ダンプモードでストレージミニポートドライバーのイメージをデバッガーで確認すると、ドライバー名の先頭に "dump\_" というプレフィックスが付けられます。 ミニポートドライバーが休止モードの場合、ドライバー名のプレフィックスは "hiber\_" になります。

 

 




