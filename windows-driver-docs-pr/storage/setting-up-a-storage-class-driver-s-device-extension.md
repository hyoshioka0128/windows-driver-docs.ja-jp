---
title: 記憶域クラス ドライバーのデバイス拡張の設定
description: 記憶域クラス ドライバーのデバイス拡張の設定
ms.assetid: 9d050d23-39c0-406e-9f4b-2e95d388f5cf
keywords:
- 記憶域クラス ドライバー WDK、デバイスの拡張機能
- クラスのドライバー WDK の記憶域、デバイスの拡張機能
- デバイスの拡張機能の WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 171e371d910fd0bb30073fac79f818746a974488
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341196"
---
# <a name="setting-up-a-storage-class-drivers-device-extension"></a>記憶域クラス ドライバーのデバイス拡張の設定


## <span id="ddk_setting_up_a_storage_class_drivers_device_extension_kg"></span><span id="DDK_SETTING_UP_A_STORAGE_CLASS_DRIVERS_DEVICE_EXTENSION_KG"></span>


[デバイス拡張機能](https://msdn.microsoft.com/library/windows/hardware/ff543119)の各デバイスは、ストレージ クラス ドライバーによって作成されたオブジェクト、そのドライバー ストレージを提供します、デバイスの I/O の管理を使用して任意のドライバーにより決定されたデータを要求、PDO へのポインターが渡されるように[ **AddDevice**](https://msdn.microsoft.com/library/windows/hardware/ff540521)、によって返されるデバイス オブジェクトへのポインター [ **IoAttachDeviceToDeviceStack**](https://msdn.microsoft.com/library/windows/hardware/ff548300)、それ自体へのポインターを戻しますデバイス オブジェクトとなどです。

ほとんどのストレージ クラス ドライバーは、次の情報のストレージも提供します。

-   デバイスの種類に固有のタイムアウト値

    クラスのドライバーが回 SRB ポートのドライバーに送信される Srb のタイムアウト値を渡すことができます\_関数\_EXECUTE\_SCSI 要求 (を参照してください[ **SCSI\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff565393)) 各クラス ドライバーの代わりです。 ポート ドライバー返します、SRB でその**SrbStatus**メンバー SRB に設定\_状態\_タイムアウト場合ポート ドライバーが基になるドライバーに要求を送信するときに、要求が完了するまでの間隔指定されたタイムアウト値を超えています。

-   クラス ドライバーのエラー処理ルーチンへのポインター

    参照してください[記憶域クラス ドライバー IoCompletion ルーチン](storage-class-driver-s-iocompletion-routines.md)ストレージ クラス ドライバーのエラー処理の詳細についてはします。

-   このドライバーは、デバイス上のバス プロトコル エラーの数

-   センス データ用のドライバーに割り当てられたバッファーへのポインター

    クラス ドライバーは、キャッシュで固定された、非ページ プールから返される検出データのメモリを割り当てる必要があります。 ドライバーのバッファーのメモリの割り当ての詳細については、次を参照してください。[システム容量のメモリを割り当てる](https://msdn.microsoft.com/library/windows/hardware/ff540588)します。

-   ドライバーにより決定された既定値を**SrbFlags**される Srb のクラス ドライバーを設定します。

-   ドライバー設定ルック アサイド リストをされる Srb の場合にルック アサイド リスト ヘッダーへのポインターを割り当てます

    参照してください[ルック アサイド リストを使用した](https://msdn.microsoft.com/library/windows/hardware/ff565416)詳細についてはします。

-   IRP と、SRB へのポインターが割り当てられ、さらに成功する必要があります要求低エラー回復操作とページング操作のメモリ状態のために保持 (によって実行されるものなど、[記憶域クラス ドライバー ReleaseQueue日常的な](storage-class-driver-s-releasequeue-routine.md))

-   ポインター、 [**ストレージ\_アダプター\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff566346)と[**ストレージ\_デバイス\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff566971)ポート ドライバーは HBA から収集されたデータ

    クラス ドライバーが取得してこのデータを使用する方法については、次を参照してください。[記憶域クラス ドライバーいる出力ルーチン](storage-class-driver-s-getdescriptor-routine.md)します。

-   フラグの状態を示す、以前と現在 PnP、デバイスの状態間の遷移を管理するには

-   冗長電源要求の処理での作業を追加を回避するために、現在デバイスの電源状態を示すフラグ

-   システムのページング ファイルの数、デバイスに存在する場合に基づく、ドライバーによって受信された要求をポケットベルによる通知 (IRP\_MJ\_で PNP [ **IRP\_MN\_デバイス\_使用状況\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff550841))

ストレージ クラス ドライバーはせず、返されたデバイス オブジェクトのポインターを使用して記憶域ポート ドライバーを介してそのデバイスに要求を送信することはできません[ **IoAttachDeviceToDeviceStack** ](https://msdn.microsoft.com/library/windows/hardware/ff548300)で保存され、デバイスの拡張機能によって、ドライバーの*AddDevice*ルーチン。

 

 




