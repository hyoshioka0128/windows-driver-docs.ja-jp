---
title: バグ チェック 0x136 VHD_BOOT_HOST_VOLUME_NOT_ENOUGH_SPACE
description: VHD_BOOT_HOST_VOLUME_NOT_ENOUGH_SPACE のバグ チェックでは、VHD から起動中に、初期化エラーを示す 0x00000136 の値を持ちます。 VHD を拡張するための十分な空き領域がありません。
ms.assetid: B3CD91D0-EB8B-4793-AE4B-72AE94F6EC1B
keywords:
- バグ チェック 0x136 VHD_BOOT_HOST_VOLUME_NOT_ENOUGH_SPACE
- VHD_BOOT_HOST_VOLUME_NOT_ENOUGH_SPACE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- VHD_BOOT_HOST_VOLUME_NOT_ENOUGH_SPACE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e0f6d34ae5bba2ba7af7b598c2488b1ad2d07333
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520413"
---
# <a name="bug-check-0x136-vhdboothostvolumenotenoughspace"></a>バグ チェック 0x136:VHD\_ブート\_ホスト\_ボリューム\_いない\_ENOUGH\_領域


VHD\_ブート\_ホスト\_ボリューム\_いない\_ENOUGH\_領域のバグ チェックが 0x00000136 の値を持ちます。 これは、VHD から起動を試みているときに初期化エラーが発生したことを示します。 VHD をホストしているボリュームには、VHD を拡張するための十分な空き領域がありません。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="vhdboothostvolumenotenoughspace-parameters"></a>VHD\_ブート\_ホスト\_ボリューム\_いない\_ENOUGH\_空間パラメーター


| パラメーター | 説明                                 |
|-----------|---------------------------------------------|
| 1         | 0 :完全なサイズに VHD ファイルを展開できません。 |
| 2         | NT 状態コード                              |
| 3         | 予約済み                                    |
| 4         | 予約済み                                    |

 

 

 




