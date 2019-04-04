---
title: Storport I/O モデル
description: Storport I/O モデル
ms.assetid: 9220b01e-725f-4a03-87f1-402c0686cccd
keywords:
- Storport ドライバー WDK、I/O
- I/O WDK Storport
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07360d804cf18580db8865f880fc966c44ffe261
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579103"
---
# <a name="storport-io-model"></a>Storport I/O モデル


## <span id="ddk_storport_i_o_model_kg"></span><span id="DDK_STORPORT_I_O_MODEL_KG"></span>


このセクションでは、Storport ドライバーの I/O モデルについて説明し、このモデルの SCSI ポート ドライバーとは対照的です。 Storport の I/O モデルは、ことを高速バスや記憶装置の潜在的なパフォーマンスを最大限に活用するように設計するいくつかの機能で構成されます。

Storport ドライバーでは、I/O のプッシュ モデルを使用します。 これは、ドライバーが入力を要求するミニポート ドライバーを待つことがなく、重複するパケットの最大数までのミニポート ドライバーに非同期 I/O 要求を転送することを意味します。 プッシュ モデルでは、ポート、ドライバーは、I/O 要求のフローを制御し、ミニポート ドライバーに要求をプッシュします。

その一方で、SCSI ポート ドライバーは、I/O のプル モデルを使用します。 I/O のプル モデルでは、SCSI ポート ドライバーは、ミニポート ドライバーへの I/O 要求を同期的に転送し、[次へ] の I/O 要求を送信する前に、新しい入力を要求するミニポート ドライバーに待機します。 さらに、ミニポート ドライバーでは、I/O 要求のフローを制御し、ポート ドライバーからの要求をプルダウンします。

SCSI ポート ドライバーの I/O モデルの詳細については、[SCSI ポート I/O モデル](scsi-port-i-o-model.md)を参照してください。

このセクションで取り上げるトピックは次のとおりです。

[全二重モード](full-duplex-mode.md)

[半二重モード:製品出荷に適していません](half-duplex-mode--not-appropriate-for-shipped-products.md)

[同期されていない HwStorBuildIo ルーチン](unsynchronized-hwstorbuildio-routine.md)

[同期されていないミニポート ドライバー ルーチン内の同期アクセス](synchronized-access-within-unsynchronized-miniport-driver-routines.md)

[Storport の I/O モデル内のスキャッター/ギャザー リストへのアクセス](access-to-scatter-gather-lists-in-the-storport-i-o-model.md)

[Storport の I/O モデルのマッピングのバッファーの使用](use-of-mapping-buffers-in-the-storport-i-o-model.md)

[パフォーマンスのヒント:HwStartIo 期間中の要求の完了](performance-tip--completing-requests-during-hwstartio.md)

[前処理および後処理の Cdb とセンス コード](pre--and-post-processing-of-cdbs-and-sense-codes.md)

 

 




