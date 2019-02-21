---
title: SCSI センス データの送信に SCSI ポートのロール
description: SCSI センス データの送信に SCSI ポートのロール
ms.assetid: 27acaa0f-5b8f-43a3-9c2b-d23943114335
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b09b4a68ca4d277ef0036e313ef6fee7870296e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527222"
---
# <a name="scsi-ports-role-in-transmitting-scsi-sense-data"></a>SCSI センス データの送信に SCSI ポートのロール


## <span id="ddk_scsi_ports_role_in_transmitting_scsi_sense_data_kg"></span><span id="DDK_SCSI_PORTS_ROLE_IN_TRANSMITTING_SCSI_SENSE_DATA_KG"></span>


SCSI ポート ドライバーは、クラス ドライバーなどの上位のコンポーネントが要求されるたびに、デバイスのデバイスの 2 つの要求のセンス データのクエリを実行します。 センス データを要求する上位のコンポーネントがで指定された長さのバッファーを指定する必要があります、 **SenseInfoBufferLength**によって示される要求のセンス データを保持するために SRB のメンバー、 **SenseInfoBuffer** 、SRB のメンバー。 SCSI ポートは、これら 2 つのフィールドは、受信した各 SRB で定義されているかどうかを判断します。 定義されている場合、SCSI ポートは、ターゲット コント ローラーでは、条件の確認を返します、SRB に応答するたびにデバイスの 2 つの要求のセンス データを提供します。

SCSI ポートが指すバッファーに格納する前に、適切な SRB 形式に要求のセンス データを変換することも、 **SenseInfoBuffer**します。

SCSI ポート IRP の完了時\_MJ\_、SRB に関連付けられている SCSI IRP、設定して要求センス情報を返すことを示す必要がありますが、 **SrbStatus** SRB に SRB のメンバー\_ステータス\_AUTOSENSE\_有効です。

 

 




