---
title: 記憶域クラス ドライバーでの PnP 初期化の処理
description: 記憶域クラス ドライバーでの PnP 初期化の処理
ms.assetid: 472e52c8-a214-418b-a82f-fd4a9bcc894e
keywords:
- 記憶域クラス ドライバー WDK、PnP
- ドライバー WDK の記憶域クラス PnP
- PnP WDK ストレージ
- プラグ アンド プレイ WDK ストレージ
- 記憶域クラス ドライバーの初期化
- 記憶域クラス ドライバー WDK、初期化しています
- ドライバー WDK の記憶域クラスの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3325e8fe680e9a34fd46bd1b343212f180c920b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390904"
---
# <a name="handling-pnp-initialization-in-a-storage-class-driver"></a>記憶域クラス ドライバーでの PnP 初期化の処理


## <span id="ddk_handling_pnp_initialization_in_a_storage_class_driver_kg"></span><span id="DDK_HANDLING_PNP_INITIALIZATION_IN_A_STORAGE_CLASS_DRIVER_KG"></span>


ストレージ クラス ドライバーの初期化は、任意の PnP ドライバーの初期化とほぼ同じです。

PnP マネージャーがドライバーを呼び出すときに、記憶域クラス ドライバーの初期化が開始されます[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチンを読み込み、ドライバーを初期化します。 記憶域クラス ドライバーの PnP マネージャーし[ **AddDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540521)日常的な物理デバイス オブジェクト (PDO) へのポインターを渡すターゲット デバイスを表します。

その*AddDevice*クラス ドライバーのルーチンを呼び出す[ **IoGetAttachedDeviceReference** ](https://msdn.microsoft.com/library/windows/hardware/ff549145) 、SRB の問題と\_関数\_要求\_デバイス コマンド (を参照してください[ **SCSI\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff565393)) デバイス オブジェクトに返される、従来のクラス ドライバーがデバイスを要求するを防ぐためにします。 クラス ドライバーする必要がありますいない他のコマンドを送信、デバイスの初期化には、このフェーズ中に。

その機能のデバイス オブジェクト (FDO) を作成し、呼び出すことによって、デバイス スタックにアタッチしますクラス ドライバーが正常にデバイスを要求する場合[ **IoAttachDeviceToDeviceStack** ](https://msdn.microsoft.com/library/windows/hardware/ff548300) PDO 入力します。 ときに*AddDevice*返します、ドライバーは PnP 開始要求を処理するために準備する必要があります (IRP\_MJ\_で PNP、 [ **IRP\_MN\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749))。 PnP マネージャーがドライバー スタック (を 1 つまたは複数のフィルター ドライバーのクラス ドライバーの上下階層化を含む可能性があります) を構築する完了した後、ターゲット デバイスのドライバー スタックの最上位のドライバーを開始要求を発行します。

デバイス スタックに FDO をアタッチする読み取ろうとしないでから成功の状態を返すだけクラス ドライバーでは、デバイスは要求が正常にことはできない場合、その*AddDevice*ルーチン。 PnP マネージャーを呼び出すことができますが、このようなドライバーは、デバイスの PnP 開始要求を受信しなかったが、 *AddDevice*同じまたは別のデバイス用にもう一度ルーチン。

記憶域クラス ドライバーを初期化する方法についての詳細については、次を参照してください。

[記憶域クラス ドライバー DriverEntry ルーチン](storage-class-driver-s-driverentry-routine.md)

[記憶域クラス ドライバー AddDevice ルーチン](storage-class-driver-s-adddevice-routine.md)

参照してください[プラグ アンド プレイ](https://msdn.microsoft.com/library/windows/hardware/ff547125)します。

 

 




