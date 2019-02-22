---
title: シーケンスのフラグ
description: NFC CX は、次のイベントのシーケンスの定数を定義します。
ms.assetid: AC6CE286-52F7-4FC9-9F38-CD10C1413A90
keywords:
- NFC
- 通信の近く
- proximity
- フィールドの近接近く
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
ms.openlocfilehash: 71441dadf2bb8922d6e2f1f0a1ec0b25f4c520f4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559056"
---
# <a name="sequence-flags"></a>シーケンスのフラグ


NFC CX は、次のイベントのシーケンスの定数を定義します。


### <a name="nfccxsequencepreinitflagskipconfig"></a>NFC\_CX\_シーケンス\_PRE\_INIT\_フラグ\_スキップ\_構成

0x00000001

このフラグは、NCI の初期化後に構成の更新をスキップする初期化前のシーケンスで使用されます。 このフラグは、force 構成オプションと共に使用することはできませんに注意してください。

### <a name="nfccxsequencepreinitflagforceconfig"></a>NFC\_CX\_シーケンス\_PRE\_INIT\_フラグ\_FORCE\_構成

0x00000002

このフラグは、NCI の初期化後に更新プログラムの構成を強制的に使用されます。 通常、NFC CX ではのみ、構成を更新して、コント ローラー サポート構成を保持していない場合、またはドライバーの更新後の構成が変更された場合。 ドライバーには、セッション ID を使用して現在の構成が引き続き発生します。

### <a name="nfccxsequenceinitcompleteflagredo"></a>NFC\_CX\_シーケンス\_INIT\_完了\_フラグ\_やり直し

0x00000001

このフラグは、初期化シーケンスを元に戻す init の完全なシーケンスで使用されます。 通常、クライアント ドライバーがファームウェアのダウンロードを実行または再起動が必要なハードウェアの設定を更新する場合に使用します。

### <a name="nfccxsequenceprenfceediscflagskip"></a>NFC\_CX\_シーケンス\_PRE\_NFCEE\_ディスク\_フラグ\_スキップ

0x00000001

このフラグは、NFCEE 検出の実行をスキップする NFCEE 事前探索シーケンス中に使用されます。

### <a name="nfccxsequencepreshutdownflagskipreset"></a>NFC\_CX\_シーケンス\_PRE\_シャット ダウン\_フラグ\_スキップ\_リセット

0x00000001

このフラグは、NFC CX をシャット ダウン中に、リセット、NCI を送信します。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[NFC クラスの拡張機能 (CX) リファレンス](https://msdn.microsoft.com/library/windows/hardware/dn905536)  

