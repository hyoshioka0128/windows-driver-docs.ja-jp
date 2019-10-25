---
Description: 機能コントローラーの USB 充電器のサポート
title: USB 充電器をサポートする USB フィルター ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eed716f97792d65577345ceeae9e705dcdd1e677
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844819"
---
# <a name="usb-filter-driver-for-supporting-usb-chargers"></a>USB 充電器をサポートする USB フィルター ドライバー

充電器の検出をサポートするフィルタードライバーを作成します (関数コントローラーで、インボックス Synopsys ドライバーと ChipIdea ドライバーが使用されている場合)。 独自の機能コントローラー用のクライアントドライバーを作成する場合、 [EVT_UFX_DEVICE_PROPRIETARY_CHARGER_SET_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_proprietary_charger_set_property)、EVT_UFX_DEVICE_PROPRIETARY_CHARGER_ を実装することによって、充電/アタッチ検出がクライアントドライバーに統合されます。 [RESET](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_proprietary_charger_reset)と[EVT_UFX_DEVICE_DETECT_PROPRIETARY_CHARGER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_proprietary_charger_detect)。

USB 機能スタックを使用すると、携帯電話やタブレットなどのデバイスは、USB バッテリ充電 (BC) 1.2 仕様で定義されているように、ホストと USB チャージャーに接続したときに課金されるようになります。 

- デバイスが課金に使用できるポートには、次の2種類があります。 デバイスは、デバイスに付属しているチャージャーで専用の充電ポート (DCP) を使用して課金されます。 また、デバイスが PC に接続されている場合、デバイスは標準のダウンストリームポートから、またはダウンストリームポートを充電できます。 どちらの場合も、 [USB BC 1.2 仕様](https://www.usb.org/developers/docs/devclass_docs/USB_Battery_Charging_1.2.pdf)に準拠しています。 
- 特定の充電器が仕様に従っていません。 USB 関数スタックを使用すると、デバイスは専用の USB 充電器から課金されるようになります。 

仕様に準拠した独自の充電器をサポートするには、これらの操作が必要です。 

- デバイスは、USB ホストまたはチャージャーが接続または切断されたことを検出できます。 
- デバイスは、BC 1.2 仕様で定義されているように、さまざまな USB 充電ポートを検出できます。 
- BC 1.2 仕様で定義されている USB 充電器の場合、デバイスは BC 1.2 仕様で許可されている現在の最大量で課金されます。 
- デバイスは、独自の USB 充電器を検出できます。 
- 専用 USB 充電器の場合は、デバイスが描画できる最大容量を決定します。 
- 接続されている USB ポートの種類について、オペレーティングシステムに通知します。 
- USB ホストが接続されていて、デバイスがそれ自体をホストとして構成している場合でも、デバイスが OS で USB 経由で最新の状態にならないようにします。 

これらの操作は、 [usb function class extension (UFX)/client ドライバー](developing-windows-drivers-for-usb-function-controllers.md)のペアと、usb 機能のデバイススタックに低いフィルターとして読み込まれるフィルタードライバーによって処理されます。 ドライバーは、USB ポートの検出から開始される USB 充電を管理して、充電を開始できるときにバッテリスタックに通知し、デバイスが描画できる最大量を通知します。 

ここでは、デバイススタックのアーキテクチャについて説明します。

![USB 充電](images/charger.png)

USB ポートがデバイスに接続されている場合、クライアントドライバーは、下位フィルタードライバーまたは割り込みによって通知を受け取ります。 この時点で、クライアントドライバーは USB ハードウェアと通信することによってポート検出を実行し、ポートの種類を UFX に報告します。 または、フィルタードライバーを要求することもできます。 この場合、フィルタードライバーは usb ハードウェアとの調整を行い、USB ポートの検出を実行し、検出されたポートの種類をクライアントドライバーに返し、クライアントドライバーが UFX に渡します。 

ポートの種類に基づいて、デバイスが描画できる最新の最大量が決定され、その情報が課金集計ドライバー (CAD) に送信されます。 情報は、CAD によって検証されます。 現在のが有効な場合、CAD は、指定された最大電流に対する課金を開始するために、バッテリクラスドライバーに要求を送信します。 バッテリクラスドライバーは、処理のために充電要求をバッテリ miniclass ドライバーに転送します。 充電要求で、専用のチャージャーが接続されていて、バッテリ miniclass が専有の充電器を処理することを指定した場合、miniclass ドライバーは、適切な最大電流を使用して課金することができます。 それ以外の場合、バッテリ miniclass は、CAD によって指定された最大電流にのみ課金されます。

