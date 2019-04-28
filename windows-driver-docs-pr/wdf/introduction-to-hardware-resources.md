---
title: ハードウェア リソースの概要
description: ハードウェア リソースの概要
ms.assetid: 34350031-daae-4213-b157-086a7a55e05b
keywords:
- WDK KMDF の構成を起動します。
- WDK KMDF の論理構成
- ハードウェア リソース WDK KMDF、ハードウェア リソースについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee5116f18166276c8133d2276ba6111cb539dfc9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378056"
---
# <a name="introduction-to-hardware-resources"></a>ハードウェア リソースの概要


PnP デバイス ドライバーがユーザー プラグイン後を[デバイスを列挙します](enumerating-the-devices-on-a-bus.md)1 つまたは複数が通常作成[論理構成](https://msdn.microsoft.com/library/windows/hardware/ff547012#ddk-logical-configurations-kg)デバイスを使用できるハードウェア リソースの組み合わせであります。 これらの構成を以下に示します。

-   A*ブート構成*システムの起動時にデバイスが必要なハードウェア リソースを一覧表示します。 (PnP デバイスは、この情報は提供、BIOS でします。)

-   追加の構成は、デバイスの操作に使用できます。 ドライバー グループにこれらの追加の構成、[リソース要件一覧](https://msdn.microsoft.com/library/windows/hardware/ff547012)します。 PnP マネージャーは、デバイスに割り当てるには、この一覧からリソースを最終的に選択されます。

ドライバーが論理構成で作成された後に送信する、framework し、フレームワークに送信、PnP マネージャー。

次に、PnP マネージャーでは、どのドライバーが、デバイスが必要ですし、既に読み込まれていない場合は、それらを読み込みますが決定します。 PnP マネージャーでは、確認のため、デバイスのドライバーをデバイスのハードウェア要件の一覧を送信します。 関数とフィルター ドライバーは、この一覧を変更し、マネージャー、PnP に送信できます。

PnP マネージャーでは、変更されたハードウェア要件の一覧を検査し、指定したリソースのシステムで実際に利用可能なを決定します。 PnP マネージャーがしようと、デバイスは、PnP マネージャーが別のデバイスに割り当てられていたリソースを必要とする場合[リソースを再配布](handling-requests-to-stop-a-device.md#redistributing-resources)システムのデバイス間で。

次に、PnP マネージャーを作成、[リソースの一覧](https://msdn.microsoft.com/library/windows/hardware/ff547012)、PnP マネージャーは、デバイスに割り当てる予定のリソースの一覧であります。 PnP マネージャーでは、確認のため、デバイスのドライバーをこの一覧を送信します。 この時点では、関数とフィルター ドライバーは、一覧からリソースを削除できますが、リソースを追加することはできません。

最後に、PnP マネージャーでは、デバイスにリソースを割り当てます。 フレームワークのパス、デバイスの関数とフィルター ドライバー、およびデバイスの機能のドライバーにリソースの一覧は、デバイスとドライバーのリソースにアクセスできるようにする必要がすべての初期化を実行します。

次の手順では、プロセスの詳細について説明します。

1.  [ユーザーはデバイスをプラグイン](a-user-plugs-in-a-device.md)します。

2.  バス ドライバーは、デバイスを検出し、[列挙](enumerating-the-devices-on-a-bus.md)こと。

3.  フレームワークは、バス ドライバーの[ *EvtDeviceResourcesQuery* ](https://msdn.microsoft.com/library/windows/hardware/ff540895)コールバック関数が[リソース リストを作成します](creating-a-resource-list-for-a-boot-configuration.md)デバイスのブート構成を記述します。

4.  フレームワークは、バス ドライバーの[ *EvtDeviceResourceRequirementsQuery* ](https://msdn.microsoft.com/library/windows/hardware/ff540894)コールバック関数を[リソース要件の一覧を作成します](creating-a-resource-requirements-list.md)デバイス。

5.  PnP マネージャーでは、デバイスが必要ですし、既に読み込まれていない、デバイスのドライバー スタックを作成する場合、読み込みは、どのドライバーが決定します。

6.  PnP マネージャーでは、ドライバー スタック レビューのために、デバイスのリソース要件のリストを送信します。 一覧は、ドライバー スタックを下へ移動、フレームワークの各関数とフィルター ドライバーの[ *EvtDeviceFilterRemoveResourceRequirements* ](https://msdn.microsoft.com/library/windows/hardware/ff540872)コールバック関数。 一覧は、スタックのバックアップを移動、フレームワークの各関数とフィルター ドライバーの[ *EvtDeviceFilterAddResourceRequirements* ](https://msdn.microsoft.com/library/windows/hardware/ff540870)コールバック関数。 これらのコールバック関数の両方ができる[リソース要件の一覧を変更](modifying-a-resource-requirements-list.md)します。

7.  PnP マネージャーでは、デバイスのリソース リストを作成し、確認のためのドライバー スタックに送信します。 フレームワークは各関数とフィルター ドライバーの[ *EvtDeviceRemoveAddedResources* ](https://msdn.microsoft.com/library/windows/hardware/ff540892)コールバック関数が[リソースを削除します](modifying-a-resource-list.md)をドライバーの。*EvtDeviceFilterAddResourceRequirements*コールバック関数が追加されるため、バス ドライバーは使用しません。

8.  フレームワークは、PnP マネージャーから最終的なリソースの一覧を受信し、それを格納します。

9.  ドライバーを呼び出す場合[ **WdfInterruptCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547345)割り込みオブジェクトを作成するために、フレームワークがリソースの一覧で割り込みリソースが検索され、割り込みオブジェクトに割り当てられます。

10. デバイスが初期化されていない d0 を入力すると、フレームワークの各ドライバーの[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)コールバック関数を[生変換](raw-and-translated-resources.md)入力引数として、デバイスのリソース リストのバージョン。 ドライバーがドライバーのフレームワークになるまでの有効なリソースの一覧を保存できます[ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)コールバック関数。

 

 





