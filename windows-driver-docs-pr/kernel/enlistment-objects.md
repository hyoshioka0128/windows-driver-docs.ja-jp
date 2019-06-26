---
title: 登録オブジェクト
description: 登録オブジェクト
ms.assetid: 80e61475-4bb7-4eaa-b9f1-ff95eac9bc77
keywords:
- WDK KTM 参加リスト
- WDK KTM、オブジェクトの登録
- リソース マネージャー WDK KTM、参加リストを作成します。
- カーネル トランザクション マネージャ WDK、参加リスト
- KTM WDK、参加リスト
- 参加リストの WDK KTM オブジェクト
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f05b9b278d2bb6c9d6cd344e0fc644de74b3c09
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384935"
---
# <a name="enlistment-objects"></a>登録オブジェクト


*参加オブジェクト*リソース マネージャーの表します[*参加*](transaction-processing-terms.md#ktm-term-enlistment)トランザクションにします。 リソース マネージャーは、トランザクションのイベントに関する通知を受け取ることができます、前に、resource manager を呼び出す必要があります[ **ZwCreateEnlistment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreateenlistment)トランザクションに参加リストを作成します。

KTM のセットを提供する[参加オブジェクト ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)カーネル モードのリソース マネージャーを呼び出すことができます。 KTM では、ユーザー モード アプリケーションを呼び出すことができるユーザー モード ルーチンのようなセットも提供します。 ユーザー モードのルーチンの詳細については、Microsoft Windows SDK を参照してください。

リソース マネージャーを呼び出すと、KTM は参加リスト オブジェクトを作成**ZwCreateEnlistment** (通常は、トランザクションのクライアント) から、resource manager が受信したトランザクションに参加します。

[TP コンポーネント](understanding-tps-components.md)呼び出せる[ **ZwOpenEnlistment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntopenenlistment)を参加オブジェクトに追加のハンドルを開きます。 ただし、ほとんどの TP の設計に追加の開いているハンドルが必要としません。

リソース マネージャーは、呼び出すことで、参加リストのオブジェクト ハンドルを閉じる[ **ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)します。 KTM がトランザクションを送信する前に、関連付けられているトランザクション オブジェクトがコミットされた最後のハンドルが閉じている場合\_通知\_をトランザクションの参加リストを持つすべてのリソース マネージャーにロールバック通知します。

オペレーティング システムは、最後のハンドルが閉じられ、KTM には、オブジェクトへのすべての参照がリリース後に、オブジェクトを削除します。

 

 




