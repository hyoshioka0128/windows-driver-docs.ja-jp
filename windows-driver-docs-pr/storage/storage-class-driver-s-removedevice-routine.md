---
title: 記憶域クラス ドライバーの RemoveDevice ルーチン
description: 記憶域クラス ドライバーの RemoveDevice ルーチン
ms.assetid: fbcbfbab-676a-43d3-aa63-0ea5e5f265d2
keywords:
- RemoveDevice
- クエリの削除要求の WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3deba68f840c7b39c8607d521bccdc1b5f048f44
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573348"
---
# <a name="storage-class-drivers-removedevice-routine"></a>記憶域クラス ドライバーの RemoveDevice ルーチン


## <span id="ddk_storage_class_drivers_removedevice_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_REMOVEDEVICE_ROUTINE_KG"></span>


デバイスが削除される直前には、PnP マネージャーは、クラス ドライバーの最初を呼び出します[ **DispatchPnP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch) PnP - クエリの削除要求で日常的な (IRP\_MJ\_でのPNP[。 **IRP\_MN\_クエリ\_削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551705)します。 記憶域クラス ドライバーは、次のケースのいずれかでクエリの削除要求に失敗する必要があります。

-   デバイスには、システムのページング ファイルや休止状態ファイルが含まれています。

-   ドライバーは、(たとえば、巻き戻しまたはテープを書式設定など) が取り消されないが長い操作を実行しています。

-   デバイス (作成) に未処理のハンドルがあります。

記憶域クラス ドライバーも失敗するクエリの削除要求のクラッシュ ダンプ、デバイスが要求した場合クラッシュ ダンプを無効にこのようなデバイスを削除するため。

記憶域クラス ドライバーは、状態を返す場合\_PnP マネージャーを呼び出して、クラス ドライバーのクエリの削除に応答の成功が要求*DispatchPnP* PnP 削除要求で日常的な (IRP\_MJ\_で PNP [ **IRP\_MN\_削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551738))。 記憶域クラス ドライバーの*DispatchPnP*日常的ないずれかを呼び出す内部*RemoveDevice*ルーチンまたは同じ機能のインラインを実装します。

記憶域クラス ドライバーの*RemoveDevice*ルーチンは、次を実行する必要があります。

-   メモリや、ドライバーによって割り当てられた、イベントなど、優れたリソースを解放します。

-   ドライバーによって、作成された場合は、シンボリック リンクを削除します。

-   デバイス オブジェクト (FDO) を削除します。

-   次の下位のドライバーに要求を転送します。

記憶域クラス ドライバーは、(たとえば、パーティション分割されたメディア デバイス上のパーティションを表すなど) にスタートアップ時の Pdo を作成、このような Pdo は、PnP マネージャーは、記憶域クラス ドライバーを削除要求を送信すると既に削除されています。

デバイス オブジェクトが削除された場合は、参照カウントが 0 になるまで、システムでデバイス オブジェクトが解決しないゼロ以外の参照カウントがある後に、もサイレント モードで消えます。 ストレージ クラス ドライバーは、デバイス オブジェクトが削除された後にデバイス オブジェクトへのポインターを使用して試みませんする必要があります。

削除要求の処理の詳細については、[デバイスを削除する](https://msdn.microsoft.com/library/windows/hardware/ff561046)を参照してください。

 

 




