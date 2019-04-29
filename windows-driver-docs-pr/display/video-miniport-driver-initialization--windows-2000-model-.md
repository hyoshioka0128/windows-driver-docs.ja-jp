---
title: ビデオ ミニポート ドライバーの初期化 (Windows 2000 モデル)
description: ビデオ ミニポート ドライバーの初期化 (Windows 2000 モデル)
ms.assetid: b18b5483-f11f-4533-9434-a3a4a30fb4b2
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、初期化しています
- ビデオのミニポート ドライバーの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45204b0068b630bd440580ee9b3e6b9c6e40ca89
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389650"
---
# <a name="video-miniport-driver-initialization-windows-2000-model"></a>ビデオ ミニポート ドライバーの初期化 (Windows 2000 モデル)


## <span id="ddk_video_miniport_driver_initialization_windows_2000_model__gg"></span><span id="DDK_VIDEO_MINIPORT_DRIVER_INITIALIZATION_WINDOWS_2000_MODEL__GG"></span>


ビデオのミニポート ドライバーの初期化は、NT カーネルの後に発生します*HAL*、PCI バス ドライバーなどのコアのドライバーが読み込まれ、初期化とします。 基本的なシステムの初期化シーケンス処理次のとおりです。

1.  NT カーネルと HAL の読み込みし、初期化します。

2.  PCI バス ドライバーなどの中核となるドライバーの読み込みし、初期化します。

3.  PCI バス ドライバーでは、その子の PCI 構成スペースの PCI リソース情報と、デバイス ID と仕入先 ID を取得し、システムにこの情報を報告します。

4.  PnP マネージャーでは、デバイスとベンダーの Id が認識している場合に、I/O マネージャーは、既知の場所から対応するビデオのミニポート ドライバーとビデオ ポート ドライバーを読み込みます。 PnP マネージャーで、Id が認識されない場合は、ミニポート ドライバーの場所のユーザーを要求し、この場所から読み込みます。

5.  I/O マネージャーには、ミニポート ドライバーの[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff556159)システムが指定した 2 つのルーチンは、ポインターを入力します。 **DriverEntry**割り当て、初期化、 [**ビデオ\_HW\_初期化\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff570505)ドライバー固有の構造体とアダプター固有の値、ミニポート ドライバーへのポインターなどの他のエントリ ポイントです。 **DriverEntry**はそれらのリソースがデバイスの PCI 構成領域に表示されませんが、デバイスによってデコードされる、従来のリソースの要求もする必要があります。 参照してください[と主張してレガシ リソース](claiming-legacy-resources.md)詳細についてはします。

6.  ミニポート ドライバーの**DriverEntry**関数呼び出し[ **VideoPortInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff570320)します。 **VideoPortInitialize**ミニポート ドライバーの初期化のすべてのミニポート ドライバーに共通する機能を実行します。 たとえば、非 PnP ドライバー、 **VideoPortInitialize**ミニポートの部分を確認しますビデオのドライバーで初期化\_HW\_初期化\_データ構造体では、の一部を初期化します、。デバイスのシステムで作成されたオブジェクトのパブリック メンバーは、デバイスの拡張機能、デバイス オブジェクトのメモリを割り当てますおよび収集し、デバイスの拡張機能に関連する情報を格納します。 参照してください[ビデオのミニポート ドライバーのデバイスの拡張機能 (Windows 2000 モデル)](video-miniport-driver-s-device-extension--windows-2000-model-.md)デバイス拡張機能の詳細についてはします。 PnP ドライバーについては、デバイス オブジェクトに関連するアクションは、後で発生します。

7.  ときに**VideoPortInitialize**から制御が戻る**DriverEntry**の戻り値を反映**VideoPortInitialize**呼び出し元に戻します。 ミニポート ドライバーの作成者では何もによって返される値に関する仮定しないように注意して**VideoPortInitialize**します。

この時点では、システムが読み込まれ、ビデオのミニポート ドライバーを初期化します。 次の手順は、デバイスを開始する PnP マネージャーです。 参照してください[ビデオのミニポート ドライバーのデバイスを起動](starting-the-device-of-the-video-miniport-driver.md)詳細についてはします。

 

 





