---
title: バッテリ ミニクラス ドライバーの DispatchSystemControl ルーチン
description: バッテリ ミニクラス ドライバーの DispatchSystemControl ルーチン
ms.assetid: bb9bb04e-4284-4e9c-85ea-60f99a01d7d9
keywords:
- バッテリ miniclass ドライバー WDK、ルーチン
- DispatchSystemControl ルーチン
- WMI の WDK バッテリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b32abd24c8dfe06a7423225ac577f1028f9bac3c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335245"
---
# <a name="dispatchsystemcontrol-routine-of-a-battery-miniclass-driver"></a>バッテリ ミニクラス ドライバーの DispatchSystemControl ルーチン


## <span id="ddk_dispatchsystemcontrol_routine_of_battery_miniclass_driver_dg"></span><span id="DDK_DISPATCHSYSTEMCONTROL_ROUTINE_OF_BATTERY_MINICLASS_DRIVER_DG"></span>


バッテリ miniclass ドライバーをサポートする必要があります[Windows Management Instrumentation](https://msdn.microsoft.com/library/windows/hardware/ff547139) (WMI) を指定して、 [ *DispatchSystemControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch) を処理するルーチン[ **IRP\_MJ\_システム\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550813) IRP します。 WMI では、測定とインストルメンテーション データを公開するドライバーを一貫した方法を提供します。

バッテリ miniclass ドライバーを使用して、 [ **BatteryClassSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff536270)ルーチンを初期処理を実行します。 **BatteryClassSystemControl**は、 *WmiLibContext*パラメーターで、関数のディスパッチ テーブルを指定します。 ルーチンを使用して、 **MinorFunction** IRP のメンバー\_MJ\_システム\_どのディスパッチ関数が呼び出しを決定するコントロール。

特定の WMI クエリ バッテリ デバイスのすべてのドライバーを処理する必要があります。 バッテリ miniclass ドライバーは、これらの WMI クエリを直接サポートが、代わりにそれらを処理するために、バッテリのクラス ドライバーに転送する必要はありません。 Miniclass ドライバーがへのポインターを提供する WMI クエリを処理するために、 [ **DpWmiQueryDataBlock** ](https://msdn.microsoft.com/library/windows/hardware/ff544096)で日常的な**QueryWmiDataBlock**のメンバー [ **WMILIB\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff565813)します。 Miniclass ドライバーは、他の種類の WMI 要求を処理する必要はありません。 そうでない場合、ドライバーは WMILIB の他のメンバーを設定\_コンテキストをゼロにします。

内でその[ **DpWmiQueryDataBlock** ](https://msdn.microsoft.com/library/windows/hardware/ff544096) miniclass ドライバーのルーチンを呼び出し、 [ **BatteryClassQueryWmiDataBlock** ](https://msdn.microsoft.com/library/windows/hardware/ff536268)ルーチンを可能な場合は、WMI のクエリ要求を処理するために、バッテリのクラス ドライバーを使用できます。 バッテリ クラス ドライバーは、その WMI クラスの GUID を処理する場合は、IRP を完了します。 それ以外の場合、 **BatteryClassQueryWmiDataBlock**状態の値を返します\_WMI\_GUID\_いない\_が見つかりました。 Miniclass ドライバーが次に、そのドライバー固有の処理を実行しを使用して、 [ **WmiCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff565798)要求を完了します。

バッテリ miniclass ドライバーがすべて WMI IRP が通話を超える処理を実行する必要はありません**BatteryClassQueryWmiDataBlock**します。 WMI の場合は、バッテリ miniclass ドライバーでは、処理の最小限の実装で**BatteryClassQueryWmiDataBlock**ステータスを返します\_WMI\_GUID\_いない\_miniclass が見つかりましたドライバーを呼び出すだけです[ **WmiCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff565798)状態のステータス値を持つ\_WMI\_GUID\_いない\_が見つかりました。

 

 




