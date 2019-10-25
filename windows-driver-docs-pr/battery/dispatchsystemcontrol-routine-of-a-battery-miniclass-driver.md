---
title: バッテリ ミニクラス ドライバーの DispatchSystemControl ルーチン
description: バッテリ ミニクラス ドライバーの DispatchSystemControl ルーチン
ms.assetid: bb9bb04e-4284-4e9c-85ea-60f99a01d7d9
keywords:
- バッテリ miniclass ドライバー WDK、ルーチン
- DispatchSystemControl ルーチン
- WMI WDK バッテリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26d4795a016934e4a895395a4560753edc1ac5ef
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829911"
---
# <a name="dispatchsystemcontrol-routine-of-a-battery-miniclass-driver"></a>バッテリ ミニクラス ドライバーの DispatchSystemControl ルーチン


## <span id="ddk_dispatchsystemcontrol_routine_of_battery_miniclass_driver_dg"></span><span id="DDK_DISPATCHSYSTEMCONTROL_ROUTINE_OF_BATTERY_MINICLASS_DRIVER_DG"></span>


バッテリ miniclass ドライバーは、 [**irp\_MJ\_システム\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)の irp を処理するために[*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンを指定することによって[Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi) (WMI) をサポートする必要があります。 WMI は、ドライバーが測定とインストルメンテーションデータを公開するための一貫した方法を提供します。

バッテリ miniclass ドライバーは、 [**BatteryClassSystemControl**](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclasssystemcontrol)ルーチンを使用して初期処理を実行します。 **BatteryClassSystemControl**は、関数のディスパッチテーブルを指定する*Wmbf bcontext*パラメーターを受け取ります。 このルーチンでは、IRP\_MJ\_システム\_コントロールの**Minorfunction**メンバーを使用して、呼び出すディスパッチ関数を決定します。

バッテリデバイス用のすべてのドライバーで処理する必要がある特定の WMI クエリがあります。 バッテリ miniclass ドライバーは、これらの WMI クエリを直接サポートする必要はありませんが、代わりにバッテリクラスドライバーに転送して処理します。 WMI クエリを処理するために、miniclass ドライバーは、 [**wm/b\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)の**query**のメンバーロックのメンバーに[**ある、の**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)オブジェクトへのポインターを提供します。 Miniclass ドライバーは、他の種類の WMI 要求を処理する必要はありません。 そうでない場合、ドライバーは、WM/b\_コンテキストの他のメンバーを0に設定します。

Miniclass ドライバーは、 [**BatteryClassQueryWmiDataBlock**](https://docs.microsoft.com/windows/desktop/api/batclass/nf-batclass-batteryclassquerywmidatablock) [**ルーチンを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)呼び出して、可能であれば、バッテリクラスドライバーが WMI クエリ要求を処理できるようにします。 バッテリクラスドライバーがその WMI クラス GUID を処理する場合は、IRP を完了します。 それ以外の場合、 **BatteryClassQueryWmiDataBlock**は WMI\_GUID\_\_状態の値を返し\_見つかりませんでした。 次に、miniclass ドライバーはドライバー固有の処理を実行し、 [**WmiCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmicompleterequest)を使用して要求を完了することができます。

バッテリ miniclass ドライバーは、 **BatteryClassQueryWmiDataBlock**を呼び出していない WMI IRP 処理を行うためには必要ありません。 バッテリ miniclass ドライバーの WMI 処理の最小実装では、 **BatteryClassQueryWmiDataBlock**によってステータス\_WMI\_GUID\_返され\_見つからない場合、miniclass ドライバーは単に[**WmiCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmicompleterequest)を呼び出します。状態の値が\_WMI\_GUID\_見つかりませ\_んでした。

 

 




