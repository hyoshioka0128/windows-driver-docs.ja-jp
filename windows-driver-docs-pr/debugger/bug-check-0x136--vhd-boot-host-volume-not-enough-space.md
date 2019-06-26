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
ms.openlocfilehash: c445fd277c8d61f4a5aa7c59e564490dd4ab5077
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367846"
---
# <a name="bug-check-0x136-vhdboothostvolumenotenoughspace"></a>バグ チェック 0x136:VHD\_ブート\_ホスト\_ボリューム\_いない\_ENOUGH\_領域


VHD\_ブート\_ホスト\_ボリューム\_いない\_ENOUGH\_領域のバグ チェックが 0x00000136 の値を持ちます。 これは、VHD から起動を試みているときに初期化エラーが発生したことを示します。 VHD をホストしているボリュームには、VHD を拡張するための十分な空き領域がありません。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="vhdboothostvolumenotenoughspace-parameters"></a>VHD\_ブート\_ホスト\_ボリューム\_いない\_ENOUGH\_空間パラメーター


| パラメーター | 説明                                 |
|-----------|---------------------------------------------|
| 1         | 0 :完全なサイズに VHD ファイルを展開できません。 |
| 2         | NT 状態コード                              |
| 3         | 予約済み                                    |
| 4         | 予約済み                                    |

 

 

 




