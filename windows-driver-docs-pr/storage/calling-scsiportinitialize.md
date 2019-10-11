---
title: ScsiPortInitialize の呼び出し
description: ScsiPortInitialize の呼び出し
ms.assetid: a736f279-9ade-4043-90f7-209fca260a39
keywords:
- ScsiPortInitialize
- SCSI ミニポートドライバーの初期化
- SCSI ミニポートドライバー WDK ストレージ、初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d958565008c9f088d17100a49dc8b3cd3da7242b
ms.sourcegitcommit: 5f4252ee4d5a72fa15cf8c68a51982c2bc6c8193
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252447"
---
# <a name="calling-scsiportinitialize"></a>ScsiPortInitialize の呼び出し


## <span id="ddk_calling_scsiportinitialize_kg"></span><span id="DDK_CALLING_SCSIPORTINITIALIZE_KG"></span>


ミニポートドライバーの HBA を複数の種類の i/o バスに接続できる場合、ミニポートドライバーは、各バスの種類に対して[**ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportinitialize)を呼び出す必要があり、各バスの種類に対して異なる*HwScsiFindAdapter*ルーチンを持つことができます。

**ScsiPortInitialize**を呼び出すたびに、このようなミニポートドライバーは次のことを行う必要があります。

-   AdapterInterfaceType メンバーを変更します。

-   [**Sas @ no__t-2INITIALIZATION @ no__t-3DATA (SCSI)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_hw_initialization_data)の HwScsiFindAdapter メンバーを変更します。これは、ミニポートドライバーがそのバスの種類に対して異なる HwScsiFindAdapter ルーチンを使用している場合に使用します。

-   新しいバスの種類に対して、ミニポートドライバーによって提供されるコンテキストデータを変更します。

-   サポートされている HBA が接続されている可能性のあるバスの種類ごとに ScsiPortInitialize を呼び出します。

ミニポートドライバーがプラグアンドプレイをサポートしていないレガシドライバーである場合、 **ScsiPortInitialize**はミニポートドライバーの*HwScsiFindAdapter*ルーチンを1回以上呼び出し、ミニポートドライバーの[**driverentry**](scsi-miniport-driver-s-driverentry-routine.md)に制御を戻します。ルーチン. すべての[*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))呼び出しは、 **ScsiPortInitialize**という順序**driverentry**のミニポートドライバーの**driverentry**ルーチンのコンテキストで行われます。

ミニポートドライバーでプラグアンドプレイがサポートされている場合、 **ScsiPortInitialize**は、今後使用するために初期化データを格納し、ステータス @ NO__T-1success をミニポートドライバーの**driverentry**ルーチンに返します。 ポートドライバーは、ミニポートドライバーがサービスとして登録されている HBA をプラグアンドプレイマネージャーが検出するまで、ミニポートドライバーの*HwScsiFindAdapter*ルーチンを呼び出しません。

プラグアンドプレイとレガシミニポートドライバーの両方について、ポートドライバーは、ミニポートドライバーの*HwScsiFindAdapter*ルーチンを呼び出す前に、次のすべてを実行します。

-   HW @ no__t-0INITIALIZATION @ no__t-1DATA の有効性を確認します。

-   は、関連する情報を収集し、デバイスオブジェクトのデバイス拡張機能に格納して、HBA を表すために作成します。

-   にメモリを割り当て、は、要求されたサイズのデバイス拡張を0で初期化します。これにより、ミニポートドライバーは、ドライバーによって決定された HBA に関する情報を格納できます。

-   **Sizeof**([**ポート @ NO__T-3configuration @ NO__T-4information**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_port_configuration_information)) の構成情報バッファーにメモリを割り当てます。

-   構成情報バッファーでは、ポート @ no__t-0CONFIGURATION @ no__t-1INFORMATION 構造体に、可能な限り特定の i/o バス上の HBA に関する構成情報を入力します。これには、ミニポートドライバーで指定された HW @ no__ を使用します。t-sql の初期化 @ no__t-3DATA とその他のソース (レガシミニポートドライバーの場合はレジストリ、プラグアンドプレイミニポートドライバーの場合はプラグアンドプレイマネージャー)。

ミニポートドライバーの*HwScsiFindAdapter*ルーチンの詳細については、「 [SCSI ミニポートドライバーの HwScsiFindAdapter ルーチン](scsi-miniport-driver-s-hwscsifindadapter-routine.md)」を参照してください。

ミニポートドライバーの**Driverentry**ルーチンによって、HW @ NO__T-2initialization @ NO__T-3data に特定の**AdapterInterfaceType**値が設定されていても、コンピューターにその種類のバスがない場合、ポートドライバーはオペレーティングシステム固有のものを返します。このような HBA が現在のコンピューターに存在しないことを示す状態値。 このバスの種類に対して、ドライバーによって提供される*HwScsiFindAdapter*ルーチンは呼び出されません。

ミニポートドライバーの**Driverentry**ルーチンによって指定された種類の i/o バスがコンピューターにない場合、ミニポートドライバーは読み込まれたままになりません。

レガシミニポートドライバーの場合、 **ScsiPortInitialize**は、レガシミニポートドライバーの**driverentry**ルーチンに制御を返す前に、次の処理を行うことにも注意してください。

-   すべての必要なシステムオブジェクトを設定します。

-   レジストリで構成情報の取得と設定を行います。

-   ミニポートドライバーに代わってシステムリソースを割り当てます。これには、ミニポートドライバーが指定した**Deviceextensionsize**、特定の**luextensionsize**、または**srbextensionsize**によって示される量のメモリが含まれます。ミニポートドライバーは、HBA 固有の状態、論理ユニットごとの状態、または要求ごとの状態をそれぞれ管理できます。

プラグアンドプレイミニポートドライバーの場合、ポートドライバーは、ミニポートドライバーの*HwScsiFindAdapter*ルーチンがを返した後、ポートドライバーがミニポートドライバーの[*HwScsiInitialize*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557302(v=vs.85))ルーチンを呼び出す前に、これらの操作を実行します。

各 SCSI ミニポートドライバーは、デバイス拡張機能の内部構造とコンテンツ、論理ユニット拡張機能 (存在する場合)、および SRB 拡張機能 (存在する場合) を定義します。 HBA 固有のデバイス拡張機能へのポインターは、 **Driverentry**以外のすべてのシステム定義のミニポートドライバールーチンへの入力引数です。 多くの **ScsiPort * * * Xxx*ルーチンでは、このポインターを引数として指定する必要があります。

**ScsiPortInitialize**は、ミニポートドライバーの**driverentry**ルーチンからのみ呼び出すことができます。 詳細については、「 [**HW @ no__t-2INITIALIZATION @ no__t-3DATA (SCSI)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_hw_initialization_data)と[**ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportinitialize)」を参照してください。

 

 




