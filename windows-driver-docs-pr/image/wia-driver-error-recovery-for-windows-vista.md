---
title: Windows Vista の WIA ドライバー エラーからの回復
description: Windows Vista の WIA ドライバー エラーからの回復
ms.assetid: 7347cc02-e00e-418e-9ac4-8bfda7d02857
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9ae92080403be4494efab3ba45ad0fe7b229781
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529559"
---
# <a name="wia-driver-error-recovery-for-windows-vista"></a>Windows Vista の WIA ドライバー エラーからの回復





ソフトウェア、ハードウェア、または構成エラーが原因で予期しない遅延が、エラー メッセージ、または解読ハング、WIA イメージの取得プロセスには、複数のポイントがあります。 これらのエラーのほとんどは、アプリケーションがイメージ データをプレビューまたは完全なイメージのいずれかを要求する時点で発生します。 このセクションには、アプリケーションとユーザーは、これらのエラーと遅延を適切に処理できるようにするメカニズムがについて説明しますと、場合によっては、そこから回復します。 設定しようとしています。 または、デバイスのプロパティの取得中にドライバーにコールバック ルーチンが返さない場合またはその他の非転送の関連する状況の中にエラーからの回復を向上させる方法は扱いません。

このセクションの内容:

[WIA エラー処理アーキテクチャ](wia-error-handling-architecture.md)

[WIA エラー ハンドラーのキャンセル モードレスのダイアログ ボックスします。](wia-error-handler-cancellation-of-modeless-dialogs.md)

[WIA エラー ハンドラーの戻り値](wia-error-handler-return-values.md)

[WIA デバイス メッセージ](wia-device-messages.md)

[ドライバーの拡張機能の処理、WIA エラーをインストールします。](installing-a-wia-error-handling-driver-extension.md)

[WIA エラー処理の例](wia-error-handling-example.md)

Windows Vista のエラー マクロについては、[WIA 診断ログ マクロ](wia-diagnostic-log-macros.md)を参照してください。

 

 




