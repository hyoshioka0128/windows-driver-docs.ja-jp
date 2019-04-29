---
title: WDF HID ミニドライバーの作成
description: このトピックでは、Windows Driver Frameworks (WDF) を使用してヒューマン インターフェイス デバイス (HID) ミニドライバーを作成する方法について説明します。
ms.assetid: 4FEDFE4B-F3B2-4B34-80DC-84BFFA4C612B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba6ee6144018d03814bd177d9981d7b758347b32
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392716"
---
# <a name="creating-wdf-hid-minidrivers"></a>WDF HID ミニドライバーの作成


このトピックでは、Windows Driver Frameworks (WDF) を使用してヒューマン インターフェイス デバイス (HID) ミニドライバーを作成する方法について説明します。

KMDF または UMDF を使用して、HID ミニドライバーを作成することができます。 Vhidmini2 ミニドライバー サンプルから始めることをお勧めします。 この KMDF または UMDF ドライバーのサンプルをコンパイルする 2.x。

**指定する内容**

1.  下位のフィルター ドライバーを記述します*MsHidUmdf.sys* (UMDF) 用または*MsHidKmdf.sys* (KMDF) のどちらもオペレーティング システムの一部として含まれています。
2.  ダウンロードして確認、 [vhidmini2 サンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/hid/vhidmini2)します。

3.  呼び出す[ **WdfFdoInitSetFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff547273)からドライバーの[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック関数。

4.  I/O を作成する I/O を受信するキューを要求する*MsHidUmdf.sys*または*MsHidKmdf.sys*クラス ドライバーからドライバーに渡します。

5.  提供、 [ *EvtIoDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541758) IOCTL に固有のメソッドのハンドラーに分岐するコールバック関数。 説明されている Ioctl 確認[WDF HID ミニドライバー Ioctl](https://msdn.microsoft.com/library/windows/hardware/hh463977)ドライバーがデバイスの該当するものを処理することを確認してください。
6.  Umdf、ドライバーは、ACPI によって列挙された場合は、必要に応じて有効にする選択的を中断します。 デバイスのハードウェア キーでは、追加、 **EnableDefaultIdleNotificationHandler**サブキーし、1 に設定します。
7.  UMDF、に対して以下の設定[INF ディレクティブ](specifying-wdf-directives-in-inf-files.md)WDF 固有で*DDInstall* INF ファイルのセクション。

    -   **UmdfKernelModeClientPolicy**に**AllowKernelModeClients**スタックでパススルー カーネル モード ドライバーを読み込むことができるようにします。
    -   **UmdfMethodNeitherAction**に**コピー** UMDF プロセス メソッドの Ioctl ことを許可する\_どちらの種類。
    -   **UmdfFileObjectPolicy**に**AllowNullAndUnknownFileObjects**
    -   **UmdfFsContextUsePolicy**に**CanUseFsContext2**

    次に、例を示します。

    ```cpp
    [hidumdf.NT.Wdf]
    UmdfKernelModeClientPolicy = AllowKernelModeClients
    UmdfMethodNeitherAction=Copy
    UmdfFileObjectPolicy=AllowNullAndUnknownFileObjects
    UmdfFsContextUsePolicy = CanUseFsContext2
    ```

Windows 7 の UMDF HID ミニドライバーを作成する場合は、ダウンロード[Windows Driver Kit (WDK) 8.1](https://go.microsoft.com/fwlink/p/?LinkId=733614)のソース コードを取得する*HidUmdf.sys*します。 次に、UMDF 1.11 ドライバーを作成し、含める*HidUmdf.sys*および UMDF 1.11 ドライバー パッケージにします。

## <a name="architecture"></a>Architecture


HID クラス ドライバー (*HidClass.sys*) とフレームワークがミニドライバー (プラグ アンド プレイの電源管理の要求など) によって I/O 要求を処理する競合の WDM ディスパッチ ルーチンを提供します。 その結果、HID ミニドライバーは、クラスのドライバーとフレームワークの両方にリンクできません。 そのため、マイクロソフトが提供しています*MsHidUmdf.sys*と*MsHidKmdf.sys*クラスのドライバーと、ミニドライバーの間に存在する WDM ドライバーであります。

両方*MsHidUmdf.sys*と*MsHidKmdf.sys* HID クラス ドライバーの呼び出す[ **HidRegisterMinidriver** ](https://msdn.microsoft.com/library/windows/hardware/ff539835)ルーチンとして登録する、実際の HID ミニドライバーします。 これらのドライバー、デバイスの機能のドライバーとして機能し、単に渡される I/O 要求クラス ドライバーからには、ドライバー (とも呼ばれますため*パススルー ドライバー*)。 KMDF と UMDF の両方を指定する唯一のコンポーネントはパススルー ドライバー の下に位置する下位のフィルター ドライバーは HID ミニドライバーします。

|                                                                                     |                                                                                        |
|-------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| UMDF アーキテクチャ                                                                   | KMDF アーキテクチャ                                                                      |
| ![hidumdf.sys ドライバー スタック内の場所](images/UMDF-basedHIDMinidrivers.png) | ![mshidkmdf.sys ドライバー スタック内の場所](images/Framework-basedHIDMinidrivers.png) |

 

 

 





