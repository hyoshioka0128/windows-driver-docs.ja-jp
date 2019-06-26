---
title: ScsiPortInitialize の呼び出し
description: ScsiPortInitialize の呼び出し
ms.assetid: a736f279-9ade-4043-90f7-209fca260a39
keywords:
- ScsiPortInitialize
- SCSI ミニポート ドライバーの初期化
- SCSI ミニポート ドライバー WDK のストレージの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa8f7c1009ad963789f8d421e07544e6f331ab33
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368365"
---
# <a name="calling-scsiportinitialize"></a>ScsiPortInitialize の呼び出し


## <span id="ddk_calling_scsiportinitialize_kg"></span><span id="DDK_CALLING_SCSIPORTINITIALIZE_KG"></span>


ミニポート ドライバーを呼び出す必要があります、ミニポート ドライバーの HBA は、I/O バスの 2 つ以上の型に接続されていることができる場合、 [ **ScsiPortInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportinitialize)ごとに、バスの種類と、別に持つことができます*HwScsiFindAdapter*バスの種類ごとに日常的な。

各呼び出しの後**ScsiPortInitialize**、このようなミニポート ドライバーにする必要があります。

-   AdapterInterfaceType メンバーを変更します。

-   HwScsiFindAdapter メンバー変更[ **HW\_初期化\_データ (SCSI)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_hw_initialization_data)ミニポート ドライバーには、そのバスの種類の異なる HwScsiFindAdapter ルーチンが含まれている場合。

-   バスの新しい種類のミニポート ドライバーによって提供されるコンテキスト データを変更します。

-   サポートされている HBA が接続されているバスの種類ごとに ScsiPortInitialize を呼び出します。

ミニポート ドライバーは、プラグ アンド プレイをサポートしていないレガシ ドライバー場合**ScsiPortInitialize**呼び出し、ミニポート ドライバーの*HwScsiFindAdapter*日常的な 1 つまたは複数回に制御を返す前にミニポート ドライバーの[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)ルーチン。 すべての[ *HwScsiFindAdapter* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))のミニポート ドライバーのコンテキストで呼び出しが行われる**DriverEntry**順序で、日常的な**DriverEntry**と呼ばれる**ScsiPortInitialize**します。

ミニポート ドライバーがプラグ アンド プレイをサポートしている場合**ScsiPortInitialize**将来使用するための初期化データを格納し、ステータスを返します\_ミニポート ドライバーの成功**DriverEntry**ルーチンです。 ポート ドライバーには、ミニポート ドライバーは呼び出しません*HwScsiFindAdapter*プラグ アンド プレイ manager がサービスとして、ミニポート ドライバーで登録された HBA を検出するまでのルーチンです。

プラグ アンド プレイと従来のミニポート ドライバーの両方でポート ドライバーは、次のすべてのミニポート ドライバーを呼び出す前に*HwScsiFindAdapter*ルーチン。

-   ハードウェア ベースの有効性をチェック\_初期化\_データ。

-   収集し、HBA を表すために作成したデバイス オブジェクトの拡張機能でデバイスの関連情報を格納します。

-   用のメモリを割り当て、デバイスに 0 で初期化します、ミニポート ドライバーがドライバーが決定については、HBA を格納できる要求されたサイズの拡張機能。

-   構成情報バッファーにメモリを割り当てます**sizeof**([**ポート\_構成\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_port_configuration_information))。

-   構成情報バッファーでは、ポートで塗りつぶします\_構成\_ミニポート ドライバーによって提供される HWをできる限り、特定のI/OでHBAに関する多くの構成情報、情報構造体のバス\_初期化\_データとレガシ ミニポート ドライバーのレジストリなどの他のソースからまたはプラグ アンド プレイのミニポート ドライバーのプラグ アンド プレイ manager。

詳細については、ミニポート ドライバーの*HwScsiFindAdapter*ルーチンを参照してください[SCSI ミニポート ドライバー HwScsiFindAdapter ルーチン](scsi-miniport-driver-s-hwscsifindadapter-routine.md)します。

場合、ミニポート ドライバーの**DriverEntry**ルーチンは、特定の設定**AdapterInterfaceType**ハードウェア ベース値\_初期化\_残念ですが、データでその型のバスはありません、コンピューター、ポート ドライバーは、このような HBA は、現在のコンピューターに存在しないことを示すオペレーティング システム固有の状態値を返します。 ドライバーによって提供される呼び出しません*HwScsiFindAdapter*そのバスの種類のルーチンです。

ミニポート ドライバーは、コンピューターのミニポート ドライバーのによって指定された種類の I/O バスがあるない場合は、読み込むが維持されない**DriverEntry**ルーチン。

従来のミニポート ドライバーでは、ことに注意して**ScsiPortInitialize**レガシ ミニポート ドライバーの制御を返す前に、次の責任も**DriverEntry**ルーチン。

-   すべての必要なシステム オブジェクトを設定します。

-   レジストリから構成情報と設定の構成情報を取得します。

-   ミニポート ドライバーが指定したによって示されるデータ量のメモリを含む、ミニポート ドライバーの代わりには、システム リソースを割り当て、 **DeviceExtensionSize**、 **SpecificLuExtensionSize**、または**SrbExtensionSize**をミニポート ドライバーを維持できます HBA に固有の状態、lun ごとの状態、または要求ごとの状態、それぞれします。

プラグ アンド プレイのミニポート ドライバーの場合、ポート ドライバーは、ミニポート ドライバーの後にこれらの操作を実行します*HwScsiFindAdapter*ルーチンを返しますポート ドライバー呼び出し、ミニポート ドライバーの前に、 [  *。HwScsiInitialize* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557302(v=vs.85))ルーチン。

各 SCSI ミニポート ドライバーでは、内部構造とそのデバイスの拡張機能、論理ユニットの拡張機能 (ある場合)、および SRB の拡張機能 (ある場合) の内容を定義します。 HBA に固有のデバイスの拡張機能へのポインターを除くすべてのシステム定義のミニポート ドライバー ルーチンへの入力引数は、 **DriverEntry**します。 多く **ScsiPort * * * Xxx*ルーチンは、引数としてこのポインターを必要とします。

**ScsiPortInitialize**ミニポート ドライバーからのみ呼び出すことができます**DriverEntry**ルーチン。 詳細については、次を参照してください。 [ **HW\_初期化\_データ (SCSI)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_hw_initialization_data)と[ **ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportinitialize)します。

 

 




