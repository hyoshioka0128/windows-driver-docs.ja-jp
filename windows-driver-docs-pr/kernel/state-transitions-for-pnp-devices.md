---
title: PnP デバイスの状態遷移
description: PnP デバイスの状態遷移
ms.assetid: 31969515-899b-407e-ab73-f6f7f36adb85
keywords:
- PnP WDK カーネルでは、状態遷移
- プラグ アンド プレイ WDK カーネルでは、状態遷移
- 状態遷移 PnP WDK
- WDK の PnP デバイスの状態
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 595cc4ecfbfe279eb436d3e0732db3eaf70b5475
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331982"
---
# <a name="state-transitions-for-pnp-devices"></a>PnP デバイスの状態遷移


## <a href="" id="ddk-state-transitions-for-pnp-devices-kg"></a>


PnP システムでは、PnP のさまざまな状態を使用して、デバイス遷移が構成されている、開始、可能性がありますが、リソースを再調整する停止および削除された可能性があります。 このセクションでは、PnP デバイスの状態の概要を示します。 この概要は、PnP ドライバーで必要なサポートの大部分の道路マップです。 このドキュメントの他の部分では、各状態の遷移の詳細について説明します。

次の図は、デバイス、および 1 つの状態から別に、デバイスの遷移の状態、PnP 示しています。

![プラグ アンド プレイの観点からデバイスの状態を示す図](images/pnp-states.png)

開始位置として、上記の図の左上、PnP デバイスは、ユーザーがデバイスを挿入したか、またはデバイスがブート時に存在するため、システムに物理的に存在します。 デバイスはまだシステム ソフトウェアには認識されません。

PnP マネージャーと親バス ドライバーは、デバイスのソフトウェア構成を開始するには、デバイスを列挙します。 PnP マネージャーでは、可能性がありますユーザー モード コンポーネントを活用するには、識別とオプションのフィルター ドライバーの機能のドライバーを含む、デバイスのドライバー。 PnP マネージャー呼び出し、 [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ドライバーがまだ読み込まれていない場合は、各ドライバーの日常的な。 Reporting と PnP デバイス列挙の詳細については、次を参照してください。 [PnP デバイスを追加するシステムを実行して](adding-a-pnp-device-to-a-running-system.md)します。

ドライバーが初期化されると、そのデバイスを初期化するために準備が必要があります。 PnP マネージャーには、ドライバーの[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)デバイスごとに日常的なドライバーを制御します。

ドライバーが受信すると、 [ **IRP\_MN\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749)ドライバーがデバイスを起動し、I/O 要求を処理する準備ができて、PnP マネージャーからの要求デバイスです。 処理については、 **IRP\_MN\_開始\_デバイス**要求を参照してください[デバイスを起動](starting-a-device.md)します。

PnP マネージャーでは、アクティブなデバイスのハードウェア リソースを再構成する必要がある場合、は、送信[ **IRP\_MN\_クエリ\_停止\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551725)と[**IRP\_MN\_停止\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551755)デバイスのドライバーを要求します。 PnP マネージャーに指示を送信することによって、デバイスを再起動するドライバー、ハードウェア リソースを再構成して後、 [ **IRP\_MN\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749)要求。 処理については Irp を停止しを参照してください[デバイスを停止する](stopping-a-device.md)します。 (ブートに構成されたデバイスのドライバーを受信できる**IRP\_MN\_クエリ\_停止\_デバイス**と**IRP\_MN\_の停止\_デバイス**この手順は前の図に示されていませんが、デバイスが開始する前に要求します)。

Windows 98 で PnP マネージャーにも送信、/ **IRP\_MN\_クエリ\_停止\_デバイス**と**IRP\_MN\_停止\_デバイス**デバイスは無効化するときに要求します。 これらのシステム上のドライバーがまた表示される、 **IRP\_MN\_停止\_デバイス**失敗した開始後に要求します。

PnP デバイスでは、システムから物理的に削除されていますか、既に削除されている、PnP マネージャーは、デバイスのドライバーをさまざまな削除 Irp を送信をデバイスのソフトウェアの表現 (デバイス オブジェクト、およびなど) を削除します。 処理については Irp を削除しを参照してください[デバイスを削除する](removing-a-device.md)します。

ある時点ですべてのドライバーのデバイスが削除された後、PnP マネージャーは、ドライバーの[*アンロード*](https://msdn.microsoft.com/library/windows/hardware/ff564886)ルーチンとドライバーをアンロードします。

 

 




