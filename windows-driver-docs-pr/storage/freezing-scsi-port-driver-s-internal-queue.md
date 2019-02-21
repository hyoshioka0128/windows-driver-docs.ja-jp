---
title: フリーズ SCSI ポート ドライバーの内部キュー
description: フリーズ SCSI ポート ドライバーの内部キュー
ms.assetid: 8e93b7d4-8429-43ec-a439-75cfeaa95887
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31d5ad502d05dd12a0877fa9332cb3cc0b64fbe2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553521"
---
# <a name="freezing-scsi-port-drivers-internal-queue"></a>フリーズ SCSI ポート ドライバーの内部キュー


## <span id="ddk_freezing_scsi_port_drivers_internal_queue_kg"></span><span id="DDK_FREEZING_SCSI_PORT_DRIVERS_INTERNAL_QUEUE_KG"></span>


SCSI ポート ドライバーは、クラス ドライバーから調停が必要なエラーが発生するたびに、その内部キューを停止します。 レポートとクラス ドライバー、キューに残っている要求の処理を再開する前に、エラーを分析する機会を提供するクラスのドライバーにエラー状態に SCSI ポートを許可するキューを保持します。 たとえば、メディアが変更された場合は、キューに置かれた要求をキャンセルする必要がありますが、クラス ドライバーによって調停が必要です。 クラスのドライバーのみが、特定の種類のメディアの削除が、特定の要求に影響するかどうかを判断するための十分なコンテキスト情報。

記憶域クラス ドライバーの Or の場合、 **SrbFlags** SRB の特定の要求に対して\_フラグ\_いいえ\_キュー\_フリーズ、SCSI ポートはその問題の結果として、キューを停止しません特定の要求。 それ以外の場合、SCSI ポートには、次の条件のいずれかのキューがフリーズします。

-   デバイスが、要求が失敗し、SCSISTAT の状態を返します\_確認\_条件または SCSISTAT\_コマンド\_終了

-   要求がタイムアウトします。

-   バスのリセットは、デバイスの要求を実行中に発生します。

-   SCSIMESS などのバス メッセージ コマンドによって要求が終了された\_中止

SCSI ポートは、SRB のフリーズを引き起こした要求を返すことによって、キューが固定されていることを示します\_状態\_キュー\_FROZEN フラグの値設定、 **SrbStatus** SRB のメンバー。 SCSI ポートは、クラス ドライバーから新しい要求をキューに挿入しますが、キューが固定されている限り、SCSI ポートは自動検出と電源の要求以外のデバイスへの要求を転送しません。

場合、SRB\_フラグ\_バイパス\_FROZEN\_キュー フラグに設定されて、 **SrbFlags** SCSI ポート、要求のメンバーが保持されているキューをバイパスし、要求をすぐに実行します。 後続の要求を**SrbFlags** SRB には、\_フラグ\_バイパス\_FROZEN\_キューのキューをフラッシュする SCSI ポートが発生します。

高度なドライバーは、SCSI ポートを SRB を使用して、キューの解除を強制できます\_関数\_リリース\_キュー リリース キュー要求。 SRB\_関数\_フラッシュ\_キューは、すべてのキューに置かれた要求をキャンセルした後、キューを解除することもできます。

 

 




