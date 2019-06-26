---
title: HwScsiFindAdapter から制御を返す
description: HwScsiFindAdapter から制御を返す
ms.assetid: 689eae76-9b5b-438f-bbdc-5ee11c6fe737
keywords:
- HwScsiFindAdapter
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiFindAdapter
- WDK SCSI の値を返す
- 状態値は WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cda7f2b37b80c9ed48bc4e0791f986a3583bd8c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386115"
---
# <a name="returning-control-from-hwscsifindadapter"></a>HwScsiFindAdapter から制御を返す


## <span id="ddk_returning_control_from_hwscsifindadapter_kg"></span><span id="DDK_RETURNING_CONTROL_FROM_HWSCSIFINDADAPTER_KG"></span>


ときに、従来のミニポート ドライバーの[ *HwScsiFindAdapter* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557300(v=vs.85))ルーチンは、コントロールを返します[ **ScsiPortInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportinitialize) を返します**DriverEntry**日常的な場合に着信*HwScsiFindAdapter*ミニポート ドライバーが、HBA をサポートされていないことが示されます。 それ以外の場合、 **ScsiPortInitialize**レジストリ内のリソースを要求し、ミニポート ドライバーに代わって、割り込みとアダプター オブジェクトなどの必要なシステム リソースを設定します。 次に、ミニポート ドライバーの呼び出し*HwScsiInitialize*ルーチンを記載[SCSI ミニポート ドライバー HwScsiInitialize ルーチン](scsi-miniport-driver-s-hwscsiinitialize-routine.md)します。

プラグ アンド プレイのミニポート ドライバーのときに*HwScsiFindAdapter*ルーチンは、コントロールを返します、ミニポート ドライバーをアンロードする場合に、プラグ アンド プレイ マネージャが許可されているへの着信*HwScsiFindAdapter*示されますいるミニポート ドライバーでは、HBA をサポートできませんでした。 ポートのドライバーが割り込みを接続する場合は、(その他のリソースを要求し、する前に設定されていること、 *HwScsiFindAdapter*呼び出し)、ミニポート ドライバーの呼び出しと[ *HwScsiInitialize*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557302(v=vs.85))ルーチンで、HBA を初期化します。

現時点では、設定に値のほか、 [**ポート\_構成\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_port_configuration_information)、ポート ドライバーもを無効にするユーザー設定の値のレジストリをチェックまたは次のすべて。

-   HBA の同期の転送

    ポート ドライバー Or 既定**SrbFlags** SRB の HBA に保持されている\_フラグ\_を無効にする\_同期\_転送します。

-   HBA のバス切断操作

    ポート ドライバー Or 既定**SrbFlags** SRB の\_フラグ\_を無効にする\_切断します。

-   キューをタグ付け

    ポートのドライバー セット、 **TaggedQueuing** hba を保持するブール値を**FALSE**します。

-   HBA の要求の内部キュー

    ポートのドライバーの設定**FALSE** 、 **MultipleRequestPerLu** HBA に関するを保持するブール値。

内容を上書き、レジストリの直前の [無効] に値のいずれか、 *HwScsiFindAdapter*ルーチンは、ポート設定\_構成\_情報バッファー。 一時的に同期の転送を無効にするバス-切断操作、タグが付けられたキュー、および HBA 内部要求キューには、トレースの要求は、開発中のミニポート ドライバーでの処理にデバッガーを使用して簡略化できます。

NT ベースのオペレーティング システムのポート ドライバー、ポートの値が使用されるにも注意してください\_構成\_ミニポート ドライバーのによって提供される情報*HwScsiFindAdapter*ルーチンまたは他のソース (など従来のミニポート ドライバーのレジストリ)、IO を埋めるために\_SCSI\_」の説明に従って、記憶域で使用するための機能のデータ クラス ドライバー、[ストレージ クラス ドライバー](storage-class-drivers.md)します。

 

 




