---
Description: Supporting USB chargers for function controllers
title: USB 充電器をサポートする USB フィルター ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c7b689d5ea194b1464fe8092e56d9548669f863
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580160"
---
# <a name="usb-filter-driver-for-supporting-usb-chargers"></a>USB 充電器をサポートする USB フィルター ドライバー

関数のコント ローラーは、インボックス Synopsys を使用している場合は、充電器の検出をサポートしているフィルター ドライバーと ChipIdea ドライバーを記述します。 クライアント ドライバーで実装することによって充電器とアタッチの検出が統合された独自の関数のコント ローラーのクライアント ドライバーを作成する場合[EVT_UFX_DEVICE_PROPRIETARY_CHARGER_SET_PROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_proprietary_charger_set_property)、 [EVT_UFX_DEVICE_PROPRIETARY_CHARGER_RESET](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_proprietary_charger_reset)、および[EVT_UFX_DEVICE_DETECT_PROPRIETARY_CHARGER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_proprietary_charger_detect)します。

USB 関数呼び出し履歴は、スマート フォンまたはタブレットでは、ホストと USB バッテリの充電 (BC) 1.2 仕様で定義された、USB 充電器に接続すると請求をなど、デバイスを使用します。 

- 2 つの種類のデバイスが充電中に使用できるポートがあります。 デバイスは、使用、デバイスに付属する充電器で専用充電ポート (DCP) から請求できます。 または、デバイスは、ダウン ストリームの標準のポートまたは PC にデバイスが接続されている場合は、下流のポートを充電からことができます。 そのような場合の両方が準拠して、 [USB BC 1.2 仕様](http://www.usb.org/developers/docs/devclass_docs/USB_Battery_Charging_1.2.pdf)します。 
- 特定の充電器は、仕様に従っていません。 その独自の USB 充電器から請求するデバイスを USB 関数スタックにできます。 

仕様に準拠していませんし、独自の充電器をサポートするには、これらの操作が必要です。 

- デバイスが USB ホストを検出できるまたは充電器をアタッチまたはデタッチします。 
- デバイスが充電 BC で 1.2 仕様に定義されたポート別 USB を検出できません。 
- Usb 仕様の充電器 BC 1.2 で定義されている、現在 1.2 の仕様、ビジネス継続性で許可されている量の最大のデバイスの料金です。 
- デバイスは、専用の USB 充電器を検出できません。 
- 専用の USB 充電器については、デバイスを描画できる現在の最大量を決定します。 
- 接続されている USB ポートの種類について、オペレーティング システムに通知します。 
- 現在、OS での USB 経由でのプルからデバイスを防ぐため、場合でも、USB ホストが接続されているし、デバイスが、ホストの構成自体。 

これらの操作によって処理されます[USB 関数クラスの拡張機能 (UFX)/クライアント ドライバー](developing-windows-drivers-for-usb-function-controllers.md)ペアと関数の USB デバイス スタックの下位のフィルターとして読み込まれているフィルター ドライバー。 ドライバー管理、USB 充電 USB ポートの検出から課金開始し、デバイスに描画できる現在の最大量バッテリ スタックへの通知を開始しています。 

デバイス スタックのアーキテクチャの表現を次に示します。

![USB 充電中](images/charger.png)

クライアント ドライバーでは、USB ポートがデバイスに関連付けられている場合、低いフィルター ドライバーまたは割り込みによっては「通知を取得します。 この時点では、クライアント ドライバーは、USB ハードウェアとの通信でポートの検出を実行し、ポートの種類を UFX に報告します。 または、フィルター ドライバーを要求することができます。 その場合は、フィルター ドライバーは、USB ポートの検出を実行する USB ハードウェアと連携し、検出されたポートの種類をクライアント ドライバーと、クライアント ドライバーが UFX に渡しますを返します。 

ポートの種類に基づき、UFX は現在、デバイスが描画できるし、充電集計ドライバー (CAD) にその情報を送信の最大量を決定します。 CAD は、情報を検証します。 現在が有効な場合は、CAD はバッテリ クラス ドライバーを指定した最大現在まで課金が開始する要求を送信します。 バッテリ クラス ドライバーは、処理のバッテリ miniclass ドライバーに充電中の要求を転送します。 充電中の要求は、独自の充電器がアタッチされたことと、バッテリ miniclass 充電器を独自の処理を指定した場合は、miniclass ドライバーが適切に決定する最大の現在の課金を試行できます。 それ以外の場合、バッテリ miniclass は CAD で指定されている現在の最大まで充電のみことができます。

