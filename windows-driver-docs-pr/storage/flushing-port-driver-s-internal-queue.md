---
title: フラッシュ ポート ドライバーの内部キュー
description: フラッシュ ポート ドライバーの内部キュー
ms.assetid: b0e6762e-0380-4ff5-aac7-36bdb5a60aa7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e8e0d9914f9f54bb48e2a60e20cba8ede9bd24a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559911"
---
# <a name="flushing-port-drivers-internal-queue"></a>フラッシュ ポート ドライバーの内部キュー


## <span id="ddk_flushing_port_driver_s_internal_queue_kg"></span><span id="DDK_FLUSHING_PORT_DRIVER_S_INTERNAL_QUEUE_KG"></span>


SCSI ポート ドライバーには、デバイスとアダプターのキャッシュをキャッシュ データを内部的にフラッシュする上位レベルのドライバーをフラッシュの要求がサポートしています。 データの整合性を維持するために、システムがシャット ダウンする前に、内部のすべてのキャッシュをフラッシュする必要があります。 フラッシュの要求を受信するとは、SCSI ポートは、すべてのキューに置かれた要求のキャンセルを独自の内部キューにフラッシュします。

高度なドライバーは、SRB の SRB の種類を送信することによってホスト アダプターのキャッシュと SCSI ポートの内部キューをフラッシュできます\_関数\_フラッシュ\_SCSI ポート ドライバーにキュー。 この SRB を受け取ったら、SCSI ポート アダプターのホスト キャッシュをフラッシュし、し、その内部キューでのすべての要求が完了すると、 **SrbStatus** SRB にメンバーが設定\_状態\_要求\_フラッシュされました。 SCSI ポートのキューが固定されている場合、SRB\_関数\_フラッシュ\_キューにキューを解除する影響。

ストレージ ミニポート ドライバーがフラッシュの要求を処理する方法の詳細については、次を参照してください。[処理 SRB\_関数\_フラッシュと SRB\_関数\_シャット ダウン](handling-srb-function-flush-and-srb-function-shutdown.md)します。

 

 




