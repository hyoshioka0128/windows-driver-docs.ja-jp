---
title: トランザクション オブジェクト
description: トランザクション オブジェクト
ms.assetid: 124105bd-70be-49b1-8ea4-af6ba1f3cf16
keywords:
- WDK KTM、オブジェクトのトランザクション
- WDK KTM トランザクション
- トランザクション クライアント WDK KTM をトランザクションの作成
- カーネル トランザクション マネージャ WDK、トランザクション
- WDK の KTM をトランザクション
- トランザクション オブジェクト WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed57a6b79a7213dc921ac3c4c31ff6d8f4ce6c27
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560294"
---
# <a name="transaction-objects"></a>トランザクション オブジェクト


*トランザクション オブジェクト*トランザクションを表します。 トランザクション クライアント トランザクションを作成するには、何らかの動作をし、いずれかのコミットを実行します。 または、トランザクションをロールバックします。

KTM のセットを提供する[トランザクション オブジェクト ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff564831)カーネル モードのトランザクションのクライアントが呼び出すことができます。 KTM では、ユーザー モード アプリケーションを呼び出すことができるユーザー モード ルーチンのようなセットも提供します。 ユーザー モードのルーチンの詳細については、Microsoft Windows SDK を参照してください。

クライアントを呼び出すと KTM トランザクション オブジェクトが作成[ **ZwCreateTransaction**](https://msdn.microsoft.com/library/windows/hardware/ff566429)します。 クライアントは、いずれかを呼び出すことができます[ **ZwCommitTransaction** ](https://msdn.microsoft.com/library/windows/hardware/ff566420)または[ **ZwRollbackTransaction** ](https://msdn.microsoft.com/library/windows/hardware/ff567086)をコミットまたはトランザクションをロールバックします。

[TP コンポーネント](understanding-tps-components.md)呼び出すことができます[ **ZwOpenTransaction** ](https://msdn.microsoft.com/library/windows/hardware/ff567033)トランザクション オブジェクトへの追加のハンドルを開きます。

クライアントが呼び出すことでトランザクション オブジェクトへのハンドルを閉じる[ **ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)します。 KTM をトランザクション オブジェクトがコミットされる前に最後のハンドルが閉じている場合、トランザクションを送信します\_通知\_をトランザクションの参加リストを持つすべてのリソース マネージャーにロールバック通知します。

オペレーティング システムは、最後のハンドルが閉じられ、KTM には、オブジェクトへのすべての参照がリリース後に、オブジェクトを削除します。

 

 




