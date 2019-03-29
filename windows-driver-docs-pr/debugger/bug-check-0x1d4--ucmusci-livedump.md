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
ms.openlocfilehash: ecc29e7b0ce9dd4611981ee5fdee46aa6d88a118
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743461"
---
# <a name="bug-check-bug-check-0x1d4-ucmucsilivedump"></a>チェックのバグ チェック 0x1D4 をバグします。UCMUCSI\_LIVEDUMP  

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

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




