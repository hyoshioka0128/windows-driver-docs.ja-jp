---
title: SRB_FUNCTION_PNP の処理
description: SRB_FUNCTION_PNP の処理
ms.assetid: 25490320-8d6b-4c5a-a585-4f628ea72393
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77ed3adba063aad446afb0a47a36f6a798ff0b95
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538369"
---
# <a name="handling-srbfunctionpnp"></a>処理 SRB\_関数\_PNP


ポート ドライバー送信 SCSI\_PNP\_要求\_アダプターに接続されているストレージ デバイスに影響する Windows のプラグ アンド プレイ (PnP) イベントのミニポート ドライバーに通知するミニポート ドライバーに要求をブロックします。

これらの要求は、単なる PnP イベントが発生しているし、ミニポート ドライバーですべてのアクションが必要としないことの通知を表します。 ミニポート ドライバーでは、(たとえば、そのハードウェアを無効にする) などの PnP 要求のコンテキスト内で実際の作業を行うことができますが、これを行うには必要ありません。

SRB に設定されます、SRB の関数メンバー\_関数\_、PNP、SRB が SCSI の種類の構造体\_PNP\_要求\_をブロックします。

 

 




