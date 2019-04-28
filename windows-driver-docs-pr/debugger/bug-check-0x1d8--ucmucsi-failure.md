---
title: バグ チェック 0x1D8 UCMUCSI_FAILURE
description: UCMUCSI_FAILURE のバグ チェックでは、0x000001D8 の値を持ちます。 クラスの拡張機能を UCSI とエラーが発生したことを示します。
keywords:
- バグ チェック 0x1D8 UCMUCSI_FAILURE
- UCMUCSI_FAILURE
ms.date: 01/11/2019
topic_type:
- apiref
api_name:
- UCMUCSI_FAILURE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 81a4036f65d8fb92ec7ea565639aac2afe18d06a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361598"
---
# <a name="bug-check-0x1d8-ucmucsifailure"></a>バグ チェック 0x1D8:UCMUCSI\_エラー

UCMUCSI\_エラーのバグ チェックが 0x000001D8 の値を持ちます。 UCSI クラスの拡張機能でエラーが発生することを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

 
## <a name="ucmucsifailure-parameters"></a>UCMUCSI\_エラー パラメーター

|パラメーター|説明|
|-------- |---------- |
|1| エラーの種類。 値:**0x0** :UCSI コマンドは、ファームウェアが時間で、コマンドに応答しなかったためにタイムアウトしました。 **0x1** :クライアント ドライバーにエラーが返されるか、またはファームウェアには、エラー コードが返されたために、UCSI コマンドの実行が失敗しました。 |
|2| UCSI コマンドの値。 |
|3| 0 以外の場合の追加情報へのポインター (を使用して、 `dt UcmUcsiCx!UCMUCSICX_TRIAGE`)。 |
|4| 予約済み。 |

## <a name="cause"></a>原因
-----

UcmUcsi ドライバー エラーが発生しました。 ドライバーには、livedump ではなく、システムのクラッシュをトリガーする設定が見つかりました。

## <a name="resolution"></a>解決方法
-----

UCSI ファームウェアが応答していないと UcmUcsiCx が UCSI コマンドのタイムアウトまたは UCSI ファームウェアに UcmUcsiCx によって送信された重大な UCSI コマンドへの応答でエラーが示されるときに通常 UCSI コマンドが失敗します。

実行`!rcdrkd.rcdrlogdump UcmUcsiCx`のこのエラーの原因の詳細情報。 

このバグ チェックの分析に関する詳細については、ブログの投稿を参照してください。 [UCSI のデバッグ ファームウェア エラー](https://techcommunity.microsoft.com/t5/Microsoft-USB-Blog/Debugging-UCSI-firmware-failures/ba-p/283226)します。


## <a name="see-also"></a>関連項目
----------

[バグチェック コード リファレンス](bug-check-code-reference2.md)

