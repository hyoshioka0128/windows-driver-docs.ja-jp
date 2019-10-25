---
title: HwScsiFindAdapter から制御を返す
description: HwScsiFindAdapter から制御を返す
ms.assetid: 689eae76-9b5b-438f-bbdc-5ee11c6fe737
keywords:
- HwScsiFindAdapter
- SCSI ミニポートドライバー WDK 記憶域、HwScsiFindAdapter
- 戻り値 WDK SCSI
- 状態値 WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a72c85b4b0238a72da3a5289039a06a2a4fc59c4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842686"
---
# <a name="returning-control-from-hwscsifindadapter"></a>HwScsiFindAdapter から制御を返す


## <span id="ddk_returning_control_from_hwscsifindadapter_kg"></span><span id="DDK_RETURNING_CONTROL_FROM_HWSCSIFINDADAPTER_KG"></span>


レガシミニポートドライバーの[*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))ルーチンから制御が返された場合、 [**ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportinitialize)が*HwScsiFindAdapter*の呼び出しによってミニポートドライバーが見つからなかったことを示すと、 **driverentry**ルーチンに戻ります。HBA をサポートします。 それ以外の場合、 **ScsiPortInitialize**はレジストリ内のリソースを要求し、ミニポートドライバーに代わって、割り込みやアダプターオブジェクトなどの必要なシステムリソースを設定します。 次に、「 [SCSI ミニポートドライバーの HwScsiInitialize ルーチン](scsi-miniport-driver-s-hwscsiinitialize-routine.md)」で説明されているミニポートドライバーの*HwScsiInitialize*ルーチンを呼び出します。

プラグアンドプレイミニポートドライバーの*HwScsiFindAdapter*ルーチンから制御が返された場合、 *HwScsiFindAdapter*への呼び出しによってミニポートドライバーが HBA をサポートできなかったことが示された場合、プラグアンドプレイマネージャーはミニポートドライバーをアンロードできます. それ以外の場合、ポートドライバーは割り込み ( *HwScsiFindAdapter*呼び出しの前に要求されて設定されたその他のリソース) を接続し、ミニポートドライバーの[*HwScsiInitialize*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557302(v=vs.85))ルーチンを呼び出して、HBA を初期化します。

現時点では、[**ポート\_構成\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)に設定されている値に加えて、ポートドライバーは、次のいずれかまたはすべてを無効にするユーザー設定値についてもレジストリを確認します。

-   HBA での同期転送

    ポートドライバーは、HBA 用に保持されている既定の**Srbflags**を SRB\_フラグを使用して、\_同期\_転送を無効\_します。

-   HBA でのバス切断操作

    ポートドライバーは、既定の**Srbflags**と SRB\_フラグを使用して、\_切断\_無効にします。

-   タグ付きキュー

    ポートドライバーは、HBA 用に保持されている**Taggedqueuing**ブール値を**FALSE**に設定します。

-   HBA での要求の内部キュー

    ポートドライバーは、HBA に関して管理する**MultipleRequestPerLu**ブール値を**FALSE**に設定します。

レジストリで直前の "disable" 値を指定すると、 *HwScsiFindAdapter*ルーチンがポート\_構成\_情報バッファーに設定したものよりも優先されます。 同期転送、バス切断操作、タグ付きキュー、および HBA 内部要求キューを一時的に無効にすると、開発中のミニポートドライバーで、デバッガーを使用して要求処理を簡単にトレースできることに注意してください。

また、NT ベースのオペレーティングシステムポートドライバーでは、ポート\_構成の値\_、ミニポートドライバーの*HwScsiFindAdapter*ルーチンまたは他のソース (レガシミニポートの場合はレジストリなど) から提供される情報を使用します。「[記憶域クラス](storage-class-drivers.md)ドライバー」で説明されているように、記憶域クラスドライバーによって使用される IO\_SCSI\_機能データを入力するためのドライバー)。

 

 




