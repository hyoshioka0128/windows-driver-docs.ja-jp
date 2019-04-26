---
title: 内部デバイス用の UWP デバイス アプリ
description: このトピックでは、UWP デバイス アプリが内部デバイスにアクセスできる方法について説明します。
ms.assetid: 864EDABF-C734-425D-A532-A01E545E4E51
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7722bee32ecdcee22804d0bb9a1aa8ebc709826
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359508"
---
# <a name="uwp-device-apps-for-internal-devices"></a>内部デバイス用の UWP デバイス アプリ


このトピックでは、UWP デバイス アプリが内部デバイスにアクセスできる方法について説明します。 *社内デバイス*デバイス内に存在または PC のエンクロージャは統合です。

**注**  すぎる外部デバイスへのアクセスに、このトピックに記載されている一部の Api を使用できます。 このトピックでは、内部のデバイスへのアクセスを具体的には重点を置いています。 各 API に関する詳細については、次を参照してください。、 [Windows API リファレンス](https://go.microsoft.com/fwlink/p/?LinkId=250938)します。

 

## <a name="span-idaccessinginternaldevicesspanspan-idaccessinginternaldevicesspanspan-idaccessinginternaldevicesspanaccessing-internal-devices"></a><span id="Accessing_internal_devices"></span><span id="accessing_internal_devices"></span><span id="ACCESSING_INTERNAL_DEVICES"></span>内部デバイスへのアクセス


次の 3 つの方法が UWP アプリが社内のデバイスにアクセスできることがあります。

| このことをお勧めしますか。 | API                                                  | 開発者      | デバイスのメタデータが必要なのですか。    |
|--------------|------------------------------------------------------|----------------|---------------------------------|
| 〇          | デバイスのシナリオ Api (イメージのキャプチャ、スキャンなど。) | すべての開発者 | no                              |
| 〇          | デバイスのプロトコル (USB、HID など) の Api                | OEM            | [はい] (に内部デバイスのみ) |
| X           | カスタム ドライバー アクセス                                 | OEM            | ○                             |

 

## <a name="span-iddevicescenarioapisspanspan-iddevicescenarioapisspanspan-iddevicescenarioapisspandevice-scenario-apis"></a><span id="Device_scenario_APIs"></span><span id="device_scenario_apis"></span><span id="DEVICE_SCENARIO_APIS"></span>デバイス Api のシナリオ


Windows ランタイムは、組み込みまたはイメージのキャプチャ、モーション センサーのスキャン、印刷、および使用するための Api など、PC に接続されているが一般的なデバイスにアクセスするためのいくつかの Api を提供します。 これらの Api は特定のシナリオを考慮して設計されている、ためにそれらとして*デバイス シナリオ Api*します。 すべての開発者がデバイスのシナリオの Api を使用することができ、それらを使用するデバイスのメタデータは必要ありません。 Api のシナリオの詳細については、次を参照してください。[デバイス統合]( https://go.microsoft.com/fwlink/p/?LinkId=306557)します。

Api では、どのようなデバイス シナリオ以外のすべてのアクセスは、Oem (または、コンポーネント サプライヤーの Oem と連携して作業) に制限されており、システム コンテナーのデバイスのメタデータが必要です。

## <a name="span-iddeviceprotocolapisspanspan-iddeviceprotocolapisspanspan-iddeviceprotocolapisspandevice-protocol-apis"></a><span id="Device_protocol_APIs"></span><span id="device_protocol_apis"></span><span id="DEVICE_PROTOCOL_APIS"></span>デバイスのプロトコルの Api


OEM]、[コンポーネントの供給業者は、Api のシナリオで満たされていない方法で内部のデバイスにアクセスする必要がある、ときに使用できる、*デバイス プロトコル Api*します。 デバイスのプロトコル Api は UWP アプリは、USB とヒューマン インターフェイス デバイス (HID) へのアクセスに使用できる Windows ランタイム Api です。 アクセスの種類は、API ごとに異なります。

| デバイスのプロトコル API | 名前空間                                                                               | アクセスの種類                      |
|---------------------|-----------------------------------------------------------------------------------------|----------------------------------|
| USB                 | [Windows.Devices.Usb](https://go.microsoft.com/fwlink/p/?LinkId=306694)                  | 排他的読み取りと排他的書き込み |
| HID                 | [Windows.Devices.HumanInterfaceDevice](https://go.microsoft.com/fwlink/p/?LinkId=306697) | 共有の読み取りと書き込みの排他    |

 

唯一の - デバイスのプロトコルの Api の最も一般的な使用 - Microsoft クラス ドライバーを使用している周辺機器にアクセスするには、デバイスのメタデータは必要ありません。 ただし、これらの Api を使用した社内のデバイスにアクセスするメタデータが必要です。 内部のデバイスにアクセスするとき、システム コンテナーの特権を持つアプリとデバイスのメタデータでアプリを指定してください。 この要件は、Oem に内部デバイスへのアクセスを制限します。

For more info, see:

-   [USB デバイスのアプリの作成](https://go.microsoft.com/fwlink/p/?LinkId=324880)
-   [ヒューマン インターフェイス デバイス (HID) のサポート](https://go.microsoft.com/fwlink/p/?LinkId=324881)
-   [Bluetooth デバイスのサポート](https://go.microsoft.com/fwlink/p/?LinkId=324882)
-   [デバイス ドライバーの要件](step-1--create-a-uwp-device-app.md)(手順 1 のステップ バイ ステップ ガイド)
-   [デバイス メタデータを作成する](step-2--create-device-metadata.md)(ステップ 2 のステップ バイ ステップ ガイド)

## <a name="span-idcustomdriveraccessspanspan-idcustomdriveraccessspanspan-idcustomdriveraccessspancustom-driver-access"></a><span id="Custom_driver_access"></span><span id="custom_driver_access"></span><span id="CUSTOM_DRIVER_ACCESS"></span>カスタム ドライバー アクセス


Oem や Ihv いない (内部または周辺機器) デバイスにアクセスするデバイスのプロトコルの Api を使用することは、Microsoft Windows エコシステム チームとそのシナリオについて説明しますが最初に接続する必要があります。 場合によっては、Microsoft 承認されると、UWP デバイスのアプリは、カスタム ドライバーを直接アクセスできます。

カスタム ドライバー アクセスには、デバイスのメタデータが必要です。 カスタム ドライバーにアクセスするには、アプリを周辺機器のデバイスまたはシステム コンテナーの特権を持つアプリとしてのデバイスのメタデータで指定してください。 カスタム ドライバー アクセスに関する詳細については、次を参照してください。 [UWP デバイス アプリ設計のガイドを特殊なデバイス、PC に内部](https://go.microsoft.com/fwlink/p/?LinkId=306693)します。

## <a name="span-idcomponentsuppliersspanspan-idcomponentsuppliersspanspan-idcomponentsuppliersspancomponent-suppliers"></a><span id="Component_suppliers"></span><span id="component_suppliers"></span><span id="COMPONENT_SUPPLIERS"></span>コンポーネント サプライヤー


コンポーネント サプライヤーは、Oem は、内部のデバイス用の UWP デバイス アプリの開発を操作できます。 これは、いくつかの方法で発生します。

-   **コンポーネント サプライヤーが開発し、アプリを配布**:ここでは、コンポーネント サプライヤーが所有する、独自に開発し、アプリと内部のデバイスにアクセスするドライバーを分散します。 OEM は、デバイスのメタデータを所有しています。

-   **OEM を策定し、アプリを配布**:ここでは、OEM は、開発し、さまざまなコンポーネント サプライヤーの 1 つまたは複数の社内のデバイスにアクセスするアプリを配布します。 最終的には、OEM は、アプリの開発、アプリの配布、およびデバイス メタデータのメンテナンスを所有します。 コンポーネント サプライヤーは、ドライバーを所有しています。

これらのワークフローの詳細については、次を参照してください。 [UWP デバイス アプリ設計のガイドを特殊なデバイス、PC に内部](https://go.microsoft.com/fwlink/p/?LinkId=306693)します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[内蔵カメラ (UWP デバイス アプリ) の場所を識別します。](identifying-the-location-of-internal-cameras.md)

 

 






