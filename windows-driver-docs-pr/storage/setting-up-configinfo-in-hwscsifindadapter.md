---
title: HwScsiFindAdapter での ConfigInfo の設定
description: HwScsiFindAdapter での ConfigInfo の設定
ms.assetid: f9c5d23d-feab-4cc4-9cd9-29c21d4fdf0b
keywords:
- HwScsiFindAdapter
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiFindAdapter
- ConfigInfo
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79202cefaac4ad7108ab81cf057d96e661b761b0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341217"
---
# <a name="setting-up-configinfo-in-hwscsifindadapter"></a>HwScsiFindAdapter での ConfigInfo の設定


## <span id="ddk_setting_up_configinfo_in_hwscsifindadapter_kg"></span><span id="DDK_SETTING_UP_CONFIGINFO_IN_HWSCSIFINDADAPTER_KG"></span>


[ *HwScsiFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff557300)ルーチンを呼び出すことができます[ **ScsiPortGetBusData** ](https://msdn.microsoft.com/library/windows/hardware/ff564624)返されたバスの種類に固有の構成を調べるなどの情報、POS データまたは EISA 構成データでは、サポートされている HBA の。

場合、 **AccessRanges**入力ポート内の要素\_構成\_情報 (、 *ConfigInfo*バッファー) ポートのドライバーで入力されて、 *HwScsiFindAdapter*ルーチンで相対バスへのアクセスの範囲をマップする必要があります[ **ScsiPortGetDeviceBase** ](https://msdn.microsoft.com/library/windows/hardware/ff564629)に返される論理アクセス アドレスの範囲を使用して、HBA と通信します。 アドレスの範囲のアクセスは、ポート ドライバーによって指定される場合*HwScsiFindAdapter* I/O バス上の他の場所にある Hba をスキャンする必要がありません。

さらに、ポート ドライバーへのアクセスを提供する場合、値の範囲は*HwScsiFindAdapter*は使用しないで、 *HwContext*パラメーター。 このようなアクセスの範囲の値が、プラグ アンド プレイの環境を示す追加の構成については、通常付属します。 このような環境で*HwScsiFindAdapter*ミニポート ドライバーの後に呼び出される[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff552654)ルーチンが返されると、それに伴って、 *HwContext*ポインターは無効になりました。 ポート ドライバーから 0 へのアクセスの範囲の値を受信して、Hba がサポートされているため、独自のスキャンを実行する唯一のドライバーが安全に使用できます、 *HwContext*ポインター。

場合、入力[**ポート\_構成\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff563900)以外で、ミニポートドライバーによって以前に指定された構成情報が含まれていない[ **HW\_初期化\_データ (SCSI)**](https://msdn.microsoft.com/library/windows/hardware/ff557456)、 *HwScsiFindAdapter*によって返される値を使用して[ **ScsiPortGetBusData** ](https://msdn.microsoft.com/library/windows/hardware/ff564624)または、必要に応じて、設定のミニポート ドライバーで定義された既定値を**AccessRanges**要素、 **BusInterruptLevel**または**BusInterruptVector**、**もできます**または**DmaPort** HBA は、システム、DMA を使用する場合と**InitiatorBusId**します。

*HwScsiFindAdapter*呼び出す必要があります[ **ScsiPortValidateRange** ](https://msdn.microsoft.com/library/windows/hardware/ff564761)このようなミニポート ドライバーによって提供されるアクセスの範囲を安全に使用できるかどうかを確認する*する前に*バス上の HBA にアクセスします。 場合**ScsiPortValidateRange**返します**TRUE**、ミニポート ドライバーを呼び出すことができます[ **ScsiPortGetDeviceBase** ](https://msdn.microsoft.com/library/windows/hardware/ff564629)範囲をマップして、使用する、呼び出しでの論理アドレスを返す **ScsiPortRead * * * Xxx*や **ScsiPortWrite * * * Xxx* I/O バス上 HBA がサポートしているかどうかを判断します。 場合**ScsiPortValidateRange**返します**FALSE**、ミニポート ドライバーは map 関数やその相対バスへのアクセスの範囲値を使用しないでください。

同様に、ポート ドライバー nonenumerable バス上のデバイスを検出するために、プラグ アンド プレイのミニポート ドライバーを呼び出す場合、ミニポート ドライバー検証する必要がありますアクセスの範囲を呼び出す前に**ScsiPortGetDeviceBase**します。

ポート ドライバーでは、割り込みの構成情報を提供する場合、ミニポート ドライバーことに同意する必要があり、その HBA は、プログラム可能割り込みの構成をサポートしている場合は、割り込みの指定された値を使用するには、その HBA をプログラムする必要があります。 割り込みの構成が指定されていない場合、値 0 または SP の値のいずれかを示すよう\_初期化されていない\_値、ミニポート ドライバーする必要がありますか、クエリの HBA、HBA ジャンパーを使用して、割り込みの選択をサポートしているかにする必要がありますHBA が割り込みを使用しない限り、0 以外の場合の既定の割り込み構成を指定します。 割り込みの構成値が 0 では、ミニポート ドライバーがポーリング済みモードでは、その HBA を制御することを示します。

ときに*HwScsiFindAdapter* HBA を検索をサポートできますが、このルーチンの HBA に合わせて、適切なメンバーを入力する必要があり、指定された**AdapterInterfaceType**、ポート\_構成\_情報。 提供が終了範囲にアクセスできるミニポート ドライバーを入力する必要があります、 **AccessRanges**については、各変換**AccessRanges**要素のバス相対 **%rangestart**値[ **ScsiPortConvertUlongToPhysicalAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff564613)ポート範囲のバスの相対ベース アドレスを設定する前に\_構成\_情報。

サポートされている HBA の*HwScsiFindAdapter*によって返される、論理アドレス範囲にマップされたアドレスを保存する必要がありますも**ScsiPortGetDeviceBase**ミニポート ドライバーのデバイスの拡張機能で。 すべてのミニポート ドライバーを呼び出す必要があります、**ScsiPortRead * * * Xxx*と **ScsiPortWrite * * * Xxx*これらの hba に関連づけてと通信するシステムのアドレスをマップします。

各正常に検証し、マップ I/O 領域内の範囲、ミニポート ドライバーを呼び出す、**ScsiPortRead/WritePort * * * Xxx*の HBA と通信するためのルーチン。 このようなメモリ領域の範囲が各、ミニポート ドライバーの呼び出し、**ScsiPortRead/WriteRegister * * * Xxx*します。

「AT と互換性のある」HBA の*HwScsiFindAdapter* 、入力をチェックする必要があります**Atdisk.要求**メンバーと"AT"を要求しようとする値をリセットして範囲の**TRUE**します。

 

 




