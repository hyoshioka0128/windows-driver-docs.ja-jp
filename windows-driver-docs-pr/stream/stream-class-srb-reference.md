---
title: ストリーム クラス SRB リファレンス
description: ストリーム クラス SRB リファレンス
ms.assetid: fdd2de58-8825-429a-937a-0bd27a180f2a
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed2d487c9a60b6ae189192d97c2bebca40c9a969
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377806"
---
# <a name="stream-class-srb-reference"></a>ストリーム クラス SRB リファレンス


## <span id="ddk_stream_class_srb_reference_ks"></span><span id="DDK_STREAM_CLASS_SRB_REFERENCE_KS"></span>


クラスのドライバーを使用して、 [ **HW\_ストリーム\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_request_block) SRB を渡すための構造をミニドライバーに要求します。 このリファレンス セクション pSRB は、ハードウェアへのポインターを指します\_ストリーム\_要求\_ブロックのオブジェクト。 ストリーム クラス ドライバーは、ミニドライバーが指定したコールバックを呼び出すときに、このポインターを渡します。

SRB 要求とは、デバイス/インスタンスに固有またはストリームに固有です。 SRB のコマンドによって、ハードウェア ベースの追加のパラメーターを渡すことができます\_ストリーム\_要求\_をブロックします。

参照してください[デバイスに固有のコマンド コード](device-specific-command-codes.md)と[Stream に固有のコマンド コード](stream-specific-command-codes.md)します。

 

 





