---
title: Again の設定と HwScsiFindAdapter からの戻り値
description: Again の設定と HwScsiFindAdapter からの戻り値
ms.assetid: 8a9cde40-06fa-4b56-818d-63a9c71da208
keywords:
- HwScsiFindAdapter
- SCSI ミニポートドライバー WDK 記憶域、HwScsiFindAdapter
- 再び WDK SCSI
- 戻り値 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 824f3ec22fb4f79e3ae0bee3019c61d356334e68
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845232"
---
# <a name="setting-again-and-returning-from-hwscsifindadapter"></a>Again の設定と HwScsiFindAdapter からの戻り値


## <span id="ddk_setting_again_and_returning_from_hwscsifindadapter_kg"></span><span id="DDK_SETTING_AGAIN_AND_RETURNING_FROM_HWSCSIFINDADAPTER_KG"></span>


サポートされていて正常に構成された HBA の場合、 [*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))は、返された\_を返す\_SP を返します。

このセクションで説明するように、を返す前に、レガシとプラグアンドプレイの両方のミニポートドライバーの*HwScsiFindAdapter*を*再度*設定する必要があります。 ただし、ミニポートドライバーがプラグアンドプレイドライバーとして読み込まれる場合は *、もう一度*行う必要はありませんが、必要に応じて、システムがプラグアンドプレイミニポートドライバーをレガシドライバーとして実行できるように、適切に設定*する必要が*あります。

*HwScsiFindAdapter*は、*同じポート\_構成\_情報で*再度呼び出す必要があることを示すために**TRUE** *に設定する*必要があります。ただし、その他の hba が接続されている場合は、新しいデバイス拡張機能を使用します。同じ i/o バス上。

*HwScsiFindAdapter*でサポートされている HBA が見つからない場合は、*再度* **FALSE**に設定し、SP\_返さ\_\_見つからないことを確認してください。 *HwScsiFindAdapter*がサポートされている HBA を検出したにもかかわらず、入力[**ポート\_構成\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)に一貫性のない構成データ (EISA バスの無効な**DmaChannel**や**BusInterruptLevel**など) がある場合、を FALSE*に*設定し、SP を返す\_無効な\_構成\_返す必要があります。 PCI バス上の HBA の場合、 *HwScsiFindAdapter*は、システムによって提供される割り込み構成情報を受け入れる必要があります。

を**FALSE**に設定してから制御を返すことに注意して*ください*\_を返します\_が見つかり\_ませんでした。または、sp\_を返します。正しくない\_の場合は、 **SystemIoBusNumber**によって識別される特定の i/o バスを示します。入力ポート\_構成\_情報には、ミニポートドライバーがサポートできる HBA がありません。 更新されたポート\_構成\_情報を使用して再度*HwScsiFindAdapter*を呼び出して、マシンの i/o バスが同じ**である場合に別の i/o バスをスキャンするようにすることはできません。AdapterInterfaceType**。

 

 




