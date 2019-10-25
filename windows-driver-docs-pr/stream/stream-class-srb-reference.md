---
title: ストリーム クラス SRB リファレンス
description: ストリーム クラス SRB リファレンス
ms.assetid: fdd2de58-8825-429a-937a-0bd27a180f2a
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f325036947d7fbbd09bb0ab3ee6f96f56a795da
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837681"
---
# <a name="stream-class-srb-reference"></a>ストリーム クラス SRB リファレンス


## <span id="ddk_stream_class_srb_reference_ks"></span><span id="DDK_STREAM_CLASS_SRB_REFERENCE_KS"></span>


クラスドライバーは、HW の\_ストリームを使用して[ **\_ブロック構造\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)し、SRB 要求をミニドライバーに渡します。 このリファレンスセクションでは、pSRB は HW\_ストリームへのポインターを参照し、\_REQUEST\_BLOCK オブジェクトを参照します。 ストリームクラスドライバーは、ミニドライバーから提供されるコールバックを呼び出すときにこのポインターを渡します。

SRB 要求は、デバイス/インスタンス固有またはストリーム固有です。 SRB コマンドによっては、ハードウェア\_ストリーム\_要求\_ブロックに追加のパラメーターが渡される場合があります。

「[デバイス固有のコマンドコード](device-specific-command-codes.md)」と「[ストリーム固有のコマンドコード](stream-specific-command-codes.md)」を参照してください。

 

 





