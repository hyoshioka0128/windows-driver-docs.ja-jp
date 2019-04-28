---
title: TDR エラー メッセージング
description: TDR エラー メッセージング
ms.assetid: 0a29c701-2257-478d-bf2d-ca4a7edecfd0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01f3535a3ed9a6d35b63aea7eee7f95c1ab1e877
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362632"
---
# <a name="tdr-error-messaging"></a>TDR エラー メッセージング


(つまりを検出し、GPU の動作が停止した場所の状況から回復するプロセス) TDR プロセス全体を通じてデスクトップは、応答していないと、エンドユーザーが利用できないためです。 回復の最後の段階では、エンドユーザーは、画面の解像度を変更するときに発生する簡単な画面フラッシュのような簡単な画面の点滅は発生します。 オペレーティング システムでは、デスクトップが正常に回復、エンドユーザーに次の情報メッセージが表示されます。

![通知のスクリーン ショットを「ディスプレイ ドライバー応答を停止しが回復」](images/tdr-error.png)

オペレーティング システムは、イベント ビューアーのアプリケーションで上記のメッセージを記録し、デバッグ レポートの形式で診断情報を収集します。 フィードバックを提供するエンド ユーザーを選択する場合、オペレーティング システムは、Online Crash Analysis (OCA) メカニズムを通じて Microsoft にこのデバッグ レポートを返します。

 

 





