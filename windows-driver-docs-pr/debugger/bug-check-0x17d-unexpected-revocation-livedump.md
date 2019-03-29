---
title: バグ チェック 0x17D PDC_UNEXPECTED_REVOCATION_LIVEDUMP
description: PDC_UNEXPECTED_REVOCATION_LIVEDUMP のバグ チェックでは、0x0000017D の値を持ちます。 アクティベーターが予期せず失効したことを示します。
keywords:
- バグ チェック 0x17D PDC_UNEXPECTED_REVOCATION_LIVEDUMP
- PDC_UNEXPECTED_REVOCATION_LIVEDUMP
ms.date: 01/04/2019
topic_type:
- apiref
api_name:
- PDC_UNEXPECTED_REVOCATION_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e5d54509fb6141a6bda5d584c5e6b3e061ebe886
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743608"
---
# <a name="bug-check-0x17d-pdcunexpectedrevocationlivedump"></a>バグ チェック 0x17D の。PDC\_予期しない\_失効\_LIVEDUMP

PDC\_予期しない\_失効\_LIVEDUMP バグ チェックが 0x0000017D の値を持ちます。 アクティベーターが予期せず失効したことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


 ## <a name="pdcunexpectedrevocationlivedump-parameters"></a>PDC\_予期しない\_失効\_LIVEDUMP パラメーター

|パラメーター|説明|
|--- |--- |
|1| 失効したアクティベーターのクライアント ID。|
|2| 失効したアクティベーター クライアント。 |
|3| 失効したアクティブ化のインスタンス。|
|4| pdc!_PDC_CLIENT_PROCESS_INFO |


## <a name="cause"></a>原因
-----

アクティベーターが予期せず取り消されています。

調査する情報を提供する、livedump が作成されます。

(このコード決してできますの実際のバグチェック。)



## <a name="see-also"></a>関連項目
----------

[バグチェック コード リファレンス](bug-check-code-reference2.md)

 




