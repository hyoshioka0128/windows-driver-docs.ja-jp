---
title: クラス/ポート ドライバーの Dispatch(Internal)DeviceControl
description: クラス/ポート ドライバーの Dispatch(Internal)DeviceControl
ms.assetid: 94f6050d-c47e-4fb2-8b7f-afadcf12e0b8
keywords:
- ディスパッチ ルーチンの WDK カーネル、DispatchDeviceControl ルーチン
- ディスパッチ DispatchDeviceControl ルーチン
- IRP_MJ_DEVICE_CONTROL I/O 関数のコード
- デバイス制御ディスパッチ ルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a1a5821b34d1195b18ca3c2d80679204b0a5f56
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384993"
---
# <a name="dispatchinternaldevicecontrol-in-classport-drivers"></a>クラス/ポート ドライバーの Dispatch(Internal)DeviceControl





クラスとポートのペアの上位レベルのドライバーの Irp の完了できる場合があります、 [ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。 たとえばクラス ドライバー、初期化中に、収集し、後続の検索が、基になるデバイスの機能に関する情報を格納[ **IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)を要求し、したがってにより、基になるデバイス ドライバーに渡すことがなく、要求処理時間を節約します。 クラスのドライバーが IRP のパラメーターを確認し、ポート ドライバーに有効なパラメーターでのみ要求を送信する設計することも可能性があります。

クラス/ポートに密接に結合されたドライバーもドライバー固有またはデバイス固有内部 I/O 制御コードの使用できるクラス ドライバーのセットを定義できます[ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)ポート ドライバーに要求します。

たとえば、 *DispatchCreateClose*ルーチンで、システムのキーボードとマウスのクラス ドライバーを有効または、キーボードとマウスの割り込みを基になるポート ドライバーを無効にする内部デバイスのシステム定義のコントロール要求を送信します。 これらのシステム クラス ドライバーを設定する**IRP\_MJ\_内部\_デバイス\_コントロール**基になるポート ドライバーを要求します。 任意の新しいキーボードまたはこれらのシステム クラス ドライバーで相互運用マウス ポート ドライバーこれら内部パブリックのデバイスのコントロール要求もサポートする必要があります。

システムの並列クラス/ポート ドライバー モデルには、同様の機能があります。 Parallel クラスの新しいドライバーからサポートを受けるシステムのパラレル ポート ドライバーの Irp を設定して**IRP\_MJ\_内部\_デバイス\_コントロール**パブリック IOCTL で要求\_並列\_ポート\_*XXX*コードを制御します。 システムのパラレル ポート ドライバーを置き換えることができますが、新しいドライバーもこの内部パブリックのデバイスに対する制御要求のセットをサポートする必要があります。

これらの内部パブリックのデバイス制御要求の詳細については、Windows Driver Kit (WDK) でデバイス固有のマニュアルを参照してください。 プライベートの I/O 制御コードを定義する方法については、次を参照してください。 [I/O 制御コードを使用して](using-i-o-control-codes.md)します。

ポート/クラス ドライバーの密接に結合されたペアは、クラス ドライバーは、ポート ドライバーに渡すことがなく特定のデバイス制御要求の処理を処理することがあります。 新しいクラス/ポート ドライバー ペアで、クラス ドライバーの*DispatchDeviceControl*ルーチンは、次のいずれかで行うことができます。

-   I/O スタックの場所は、独自のパラメーターの有効性をチェック、任意のパラメーター エラー、および呼び出しが見つかった場合は、状態の I/O ブロックを設定[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)で、 *PriorityBoost* IO の\_いいえ\_インクリメントしますそれ以外の場合、呼び出し[ **IoGetNextIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetnextirpstacklocation)ポート ドライバーの、独自の I/O スタックの場所にコピーし、渡す、。IRP [**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)します。

-   または、何もしない複数のパラメーターをチェックせず、ポート ドライバーの IRP で I/O スタックの場所を設定し、処理のためのポート ドライバーに渡すこと。

SCSI クラス ドライバーには、デバイス制御要求を処理するための特別な要件があります。 これらの要件の詳細については、次を参照してください。[記憶装置ドライバー](https://docs.microsoft.com/windows-hardware/drivers/storage/storage-drivers)します。

 

 




