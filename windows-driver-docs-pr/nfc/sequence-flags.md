---
title: シーケンスのフラグ
description: NFC CX は、シーケンスイベントに対して次の定数を定義します。
ms.assetid: AC6CE286-52F7-4FC9-9F38-CD10C1413A90
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
topic_type:
- apiref
api_name:
- NFC_CX_SEQUENCE_PRE_INIT_FLAG_SKIP_CONFIG
- NFC_CX_SEQUENCE_PRE_INIT_FLAG_FORCE_CONFIG
- NFC_CX_SEQUENCE_INIT_COMPLETE_FLAG_REDO
- NFC_CX_SEQUENCE_PRE_NFCEE_DISC_FLAG_SKIP
- NFC_CX_SEQUENCE_PRE_SHUTDOWN_FLAG_SKIP_RESET
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45f393c9737e1184e6895883fe2fcba4d3797c38
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834004"
---
# <a name="sequence-flags"></a>シーケンスのフラグ


NFC CX は、シーケンスイベントに対して次の定数を定義します。


### <a name="nfc_cx_sequence_pre_init_flag_skip_config"></a>NFC\_CX\_SEQUENCE\_事前\_INIT\_フラグ\_構成をスキップ\_

0x00000001

このフラグは、初期化前のシーケンスで、NCI の初期化後に構成の更新をスキップするために使用されます。 注このフラグは、force 構成オプションと共に使用することはできません。

### <a name="nfc_cx_sequence_pre_init_flag_force_config"></a>NFC\_CX\_SEQUENCE\_事前\_INIT\_フラグ\_強制\_構成

0x00000002

このフラグは、NCI の初期化後に構成を強制的に更新するために使用されます。 通常、NFC CX は、コントローラーが構成の保持をサポートしていない場合、またはドライバーの更新後に構成が変更された場合にのみ、構成を更新します。 ドライバーは、セッション ID を使用して現在の構成を保持します。

### <a name="nfc_cx_sequence_init_complete_flag_redo"></a>NFC\_CX\_SEQUENCE\_INIT\_完了\_フラグ\_再実行

0x00000001

このフラグは、初期化シーケンスを再実行するために、init complete sequence で使用されます。 これは通常、クライアントドライバーが、再起動を必要とするファームウェアのダウンロードまたは更新されたハードウェア設定を実行した場合に使用されます。

### <a name="nfc_cx_sequence_pre_nfcee_disc_flag_skip"></a>NFC\_CX\_SEQUENCE\_\_NFCEE\_ディスク\_フラグ\_スキップ

0x00000001

このフラグは、NFCEE の事前検出シーケンス中に、NFCEE discovery の実行をスキップするために使用されます。

### <a name="nfc_cx_sequence_pre_shutdown_flag_skip_reset"></a>NFC\_CX\_シーケンス\_事前\_シャットダウン\_フラグ\_スキップ\_リセット

0x00000001

このフラグによって、NFC CX はシャットダウン中に NCI reset を送信しません。

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC クラス拡張 (CX) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

