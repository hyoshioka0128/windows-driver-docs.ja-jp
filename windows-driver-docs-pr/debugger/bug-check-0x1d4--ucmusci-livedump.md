---
title: バグ チェック 0x1D4 UCMUCSI_LIVEDUMP
description: UCMUCSI_LIVEDUMP ライブ ダンプには、0x000001D4 の値があります。
keywords:
- バグ チェック 0x1D4 UCMUCSI_LIVEDUMP
- UCMUCSI_LIVEDUMP
ms.date: 02/22/2019
topic_type:
- apiref
api_name:
- UCMUCSI_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a20fb9166068558322d622b99f65e3c8acf9b3f3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367570"
---
# <a name="bug-check-bug-check-0x1d4-ucmucsilivedump"></a>チェックのバグ チェック 0x1D4 をバグします。UCMUCSI\_LIVEDUMP  

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


UCMUCSI_LIVEDUMP ライブ ダンプには、0x000001D4 の値があります。 

UcmUcsi.sys ドライバー エラーが発生しました。 UcmUcsi.sys は、アドインのボックス USB コネクタ マネージャー UCSI クライアント ドライバーです。 詳細については、次を参照してください。 [USB 型 C コネクタ システム ソフトウェア インターフェイス (UCSI) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/ucsi)します。


## <a name="ucmucsilivedump-parameters"></a>UCMUCSI\_LIVEDUMP パラメーター

パラメーター | 説明 
|---------|--------------|
1 | エラーの種類-次の値を参照してください。
2 | UCSI コマンドの値。
3 | 0 以外の場合の追加情報へのポインター (dt UcmUcsiCx!UCMUCSICX_TRIAGE)。
4 | 予約済み。
 
**エラーの種類**

0x0 :UCSI コマンドは、ファームウェアが時間で、コマンドに応答しなかったためにタイムアウトしました。

0x1:クライアント ドライバーにエラーが返されるか、またはファームウェアには、エラー コードが返されたために、UCSI コマンドの実行が失敗しました。




