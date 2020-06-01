---
title: 多機能デバイス ドライバー設計ガイド
description: 多機能デバイス ドライバー設計ガイド
ms.assetid: 110c0b9b-4870-4853-8fbf-a9faf0c5f2ca
keywords:
- 多機能デバイス WDK
- 多機能デバイス WDK, 多機能デバイスについて
- 結合機能デバイス WDK
- 多機能デバイス WDK
- プリンターの多機能 WDK
- DVD/CD-ROM 多機能 WDK
- 多機能デバイス WDK , インストール
- 親バス WDK 多機能デバイス
- INF ファイル WDK 多機能デバイス
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 69588e8e53ad6872c779898765cc6ff15fa5059f
ms.sourcegitcommit: 609c5731b2db4c17b9959082c4621c001e012db1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2020
ms.locfileid: "84223555"
---
# <a name="multifunction-device-driver-design-guide"></a>多機能デバイス ドライバー設計ガイド

"*多機能デバイス*" は、その親バス上のある場所を占めますが、1 つ以上の関数が含まれています。 プリンター/スキャナー/fax デバイスおよびモデム/ネットワーク カードの組み合わせは、一般的な多機能デバイスです。

多機能デバイスでは、個々の機能は独立しています。 つまり、機能は次の特性を持つ必要があります。

- 機能には、起動順序の依存関係を設定することはできません。

- ある機能のリソース要件は、別の機能のリソースの観点から表現することはできません (たとえば、*function1* では I/O ポート *x* を使用し、*function2* ではポート *x* + 200 を使用するなど)。

- 各機能は、別の機能と同じドライバーによってサービスが提供されている場合でも、個別のデバイスとして動作できる必要があります。

- デバイス上の各機能を列挙する必要があります。

- 各機能のリソース要件は、PnP マネージャーに伝達する必要があります。

- 機能ごとに INF ファイルとドライバーが必要です。

これらの各タスクを実行するコンポーネントは、デバイスの親バスの多機能標準 (デバイスが標準に準拠する範囲で)、親バス ドライバーの機能に依存します。

デバイスがそのバスの多機能標準に準拠している場合、ドライバーの要件が大幅に減ります。 PC カードおよび PCI バスには、多機能の業界標準が定義されています。

データ記憶域のために (オーディオ/ビデオの再生のためではなく) 使用される多機能 DVD/CD-ROM デバイスを使用する場合は、デバイスを 1 つの論理単位として扱う、システムから提供される WDM DVD クラス ドライバーを使用する必要があります。

他の機能が組み合わされた多機能デバイスの場合、デバイスがそのバスの多機能標準に準拠している場合は、システムから提供されるドライバーと INF ファイルを使用できます。 システムから提供される多機能ドライバー (mf.sys) は、バス レベルの列挙と、デバイスのリソース割り当て要件を処理でき、システムから提供される INF (mf.sys) は多機能デバイスをインストールできます。 個々のデバイス機能ごとに 1 つの機能ドライバーと INF ファイルのみを指定する必要があります。

デバイスがそのバスの標準に準拠しない場合は、デバイス機能の機能ドライバーと INF ファイルだけでなく、mf.sys 機能と同等のドライバーを指定する必要があります。

多機能デバイスをインストールするには、通常、デバイスの基本 INF ファイル、各デバイス機能の追加の INF ファイルを指定します。 基本の INF ファイルは、通常、デバイスの個々の機能に対して、INF ファイルをコピーします。 これを実行する方法については、[INF のコピー](https://docs.microsoft.com/windows-hardware/drivers/install/copying-inf-files)に関するページを参照してください。

次のセクションでは、さまざまな種類の多機能デバイスのドライバーおよびインストールの要件について説明します。

[多機能 PC カード デバイスのサポート](supporting-multifunction-pc-card-devices.md)

[多機能 PCI デバイスのサポート](supporting-multifunction-pci-devices.md)

[他のバスでの多機能デバイスのサポート](supporting-multifunction-devices-on-other-buses.md)

[システム提供の多機能バス ドライバーの使用](using-the-system-supplied-multifunction-bus-driver.md)

[多機能デバイス用のリソース マップの作成](creating-resource-maps-for-a-multifunction-device.md)

INF ファイルの構文については、「[INF ファイルのセクションとディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)」を参照してください。

Windows Driver Kit (WDK) には、[多機能オーディオ デバイス](https://docs.microsoft.com/windows-hardware/drivers/audio/multifunction-audio-devices)をサポートする方法を説明する別のセクションが含まれています。
