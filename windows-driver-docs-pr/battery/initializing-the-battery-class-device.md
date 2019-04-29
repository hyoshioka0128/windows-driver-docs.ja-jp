---
title: バッテリ クラス デバイスの初期化
description: バッテリ クラス デバイスの初期化
ms.assetid: d385533e-790a-47b3-a3d2-d620cbd40a4d
keywords:
- バッテリ クラス ドライバー WDK、デバイスの初期化
- バッテリ miniclass ドライバー WDK を登録します。
- バッテリのデバイスの登録
- デバイスのバッテリの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8de76e984768e09fef10b3ac892a6ac52cc1c3d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335339"
---
# <a name="initializing-the-battery-class-device"></a>バッテリ クラス デバイスの初期化


## <span id="ddk_initializing_the_battery_class_device_dg"></span><span id="DDK_INITIALIZING_THE_BATTERY_CLASS_DEVICE_DG"></span>


[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチンがバッテリ クラスのデバイスを初期化し、クラス ドライバーを miniclass ドライバーに登録する必要があります。 そのため、miniclass ドライバーを呼び出すには、 [ **BatteryClassInitializeDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff536266)ルーチン。 この呼び出しは、2 つのドライバーのサポート ルーチンを使用できるように、クラスのドライバーと miniclass ドライバーを登録します。 この呼び出しは、複合バッテリと電源メーターでわかるようにもバッテリ デバイスと、システムに登録します。

**BatteryClassInitializeDevice**へのポインターが必要です、 [**バッテリ\_ミニポート\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff536287)次の情報を含む構造体。

-   **MajorVersion**と**MinorVersion**、この miniclass ドライバーがサポートするクラス ドライバーのメジャーおよびマイナー バージョン番号。

    バージョン番号はバッテリとして Batclass.h で定義されている\_クラス\_メジャー\_バージョンとバッテリ\_クラス\_マイナー\_バージョンについては、それぞれします。

-   **QueryTag**、miniclass ドライバーのエントリ ポイント[ *BatteryMiniQueryTag* ](https://msdn.microsoft.com/library/windows/hardware/ff536275)ルーチン。

-   **QueryInformation**、miniclass ドライバーのエントリ ポイント[ *BatteryMiniQueryInformation* ](https://msdn.microsoft.com/library/windows/hardware/ff536273)ルーチン。

-   **SetInformation**、miniclass ドライバーのエントリ ポイント[ *BatteryMiniSetInformation* ](https://msdn.microsoft.com/library/windows/hardware/ff536276)ルーチン。

-   **SetStatusNotify**、miniclass ドライバーのエントリ ポイント[ *BatteryMiniSetStatusNotify* ](https://msdn.microsoft.com/library/windows/hardware/ff536277)ルーチン。

-   **DisableStatusNotify**、miniclass ドライバーのエントリ ポイント[ *BatteryMiniDisableStatusNotify* ](https://msdn.microsoft.com/library/windows/hardware/ff536272)ルーチン。

-   **コンテキスト**、miniclass ドライバーのコンテキスト情報へのポインター。

    コンテキスト情報は、クラス ドライバーを呼び出すたびに、miniclass ドライバーに戻されるデバイス拡張機能 FDO へのポインターでは通常、 [BatteryMini*Xxx* ](https://msdn.microsoft.com/library/windows/hardware/ff536286)ルーチン。

-   **Pdo**デバイスの PDO へのポインター。

-   **DeviceName**、NULL パラメーター。PnP デバイスの名前ではありません。

この構造体を設定した後、miniclass ドライバーをアタッチします自体、バッテリ クラス ドライバーを呼び出すことによって**BatteryClassInitializeDevice**、バッテリにポインターを渡すことと\_ミニポート\_情報構造体。 代わりに、バッテリ クラス ドライバー サポート ルーチンへの後続の呼び出しで使用するを識別するハンドルを受け取ります。 Miniclass ドライバーでは、非ページ メモリで返されるクラス ハンドルを格納する必要があります。

呼び出した後**BatteryClassInitializeDevice**、 [ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチンが他のデバイスに固有のデータを初期化する必要もあります。

 

 




