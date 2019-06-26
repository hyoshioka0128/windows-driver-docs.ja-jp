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
ms.openlocfilehash: cb0a41d448e01bb13d5fe6dae95ed0d661605e3e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382941"
---
# <a name="transaction-objects"></a>トランザクション オブジェクト


*トランザクション オブジェクト*トランザクションを表します。 トランザクション クライアント トランザクションを作成するには、何らかの動作をし、いずれかのコミットを実行します。 または、トランザクションをロールバックします。

KTM のセットを提供する[トランザクション オブジェクト ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)カーネル モードのトランザクションのクライアントが呼び出すことができます。 KTM では、ユーザー モード アプリケーションを呼び出すことができるユーザー モード ルーチンのようなセットも提供します。 ユーザー モードのルーチンの詳細については、Microsoft Windows SDK を参照してください。

クライアントを呼び出すと KTM トランザクション オブジェクトが作成[ **ZwCreateTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreatetransaction)します。 クライアントは、いずれかを呼び出すことができます[ **ZwCommitTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommittransaction)または[ **ZwRollbackTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbacktransaction)をコミットまたはトランザクションをロールバックします。

[TP コンポーネント](understanding-tps-components.md)呼び出すことができます[ **ZwOpenTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntopentransaction)トランザクション オブジェクトへの追加のハンドルを開きます。

クライアントが呼び出すことでトランザクション オブジェクトへのハンドルを閉じる[ **ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)します。 KTM をトランザクション オブジェクトがコミットされる前に最後のハンドルが閉じている場合、トランザクションを送信します\_通知\_をトランザクションの参加リストを持つすべてのリソース マネージャーにロールバック通知します。

オペレーティング システムは、最後のハンドルが閉じられ、KTM には、オブジェクトへのすべての参照がリリース後に、オブジェクトを削除します。

 

 




