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
ms.openlocfilehash: ffaa8a3434cadb898297b48951fb59d38d5c687b
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606550"
---
# <a name="returning-control-from-hwscsifindadapter"></a>HwScsiFindAdapter から制御を返す

レガシミニポートドライバーの[*HwScsiFindAdapter*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))ルーチンから制御が返されると、 [**ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportinitialize)の呼び出しによって、ミニポートドライバーが HBA をサポートできなかったこと*が示され*た場合、 **driverentry**ルーチンに戻ります。 それ以外の場合、 **ScsiPortInitialize**はレジストリ内のリソースを要求し、ミニポートドライバーに代わって、割り込みやアダプターオブジェクトなどの必要なシステムリソースを設定します。 次に、「 [SCSI ミニポートドライバーの HwScsiInitialize ルーチン](scsi-miniport-driver-s-hwscsiinitialize-routine.md)」で説明されているミニポートドライバーの*HwScsiInitialize*ルーチンを呼び出します。

プラグアンドプレイミニポートドライバーの*HwScsiFindAdapter*ルーチンから制御が返された場合、 *HwScsiFindAdapter*への呼び出しによってミニポートドライバーが HBA をサポートできなかったことが示された場合、プラグアンドプレイマネージャーはミニポートドライバーをアンロードできます。 それ以外の場合、ポートドライバーは割り込み ( *HwScsiFindAdapter*呼び出しの前に要求されて設定されたその他のリソース) を接続し、ミニポートドライバーの[*HwScsiInitialize*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557302(v=vs.85))ルーチンを呼び出して、HBA を初期化します。

現時点では、 [PORT_CONFIGURATION_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)で設定されている値に加えて、ポートドライバーは、次のいずれかまたはすべてを無効にするユーザー設定値についてもレジストリを確認します。

- HBA での同期転送: ポートドライバーは、SRB_FLAGS_DISABLE_SYNCH_TRANSFER で HBA 用に保持されている既定の**Srbflags**を使用します。

- HBA でのバス切断操作: ポートドライバーは、既定の**Srbflags**を SRB_FLAGS_DISABLE_DISCONNECT で処理します。

- タグ付きキュー: ポートドライバーは、HBA 用に保持されている**Taggedqueuing**ブール値を**FALSE**に設定します。

- HBA での要求の内部キュー: ポートドライバーは、HBA に関して管理する**MultipleRequestPerLu**ブール値を**FALSE**に設定します。

レジストリで直前の "disable" 値を指定すると、PORT_CONFIGURATION_INFORMATION バッファーで設定されている*HwScsiFindAdapter*ルーチンが上書きされます。 同期転送、バス切断操作、タグ付きキュー、および HBA 内部要求キューを一時的に無効にすると、開発中のミニポートドライバーで、デバッガーを使用して要求処理を簡単にトレースできることに注意してください。

また、NT ベースのオペレーティングシステムポートドライバーでは、「[記憶域クラスドライバー](introduction-to-storage-class-drivers.md)」で説明されているように、記憶域クラスドライバーで使用する IO_SCSI_CAPABILITIES データを入力するために、ミニポートドライバーの*HwScsiFindAdapter*ルーチンまたは他のソース (レガシミニポートドライバーの場合はレジストリなど) から提供された PORT_CONFIGURATION_INFORMATION の値を使用します。
