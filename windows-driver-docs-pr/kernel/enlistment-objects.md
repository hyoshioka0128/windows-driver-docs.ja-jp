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
ms.openlocfilehash: 6a3bf610ad7d092481c462d9c453532543cb5231
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334053"
---
# <a name="enlistment-objects"></a>登録オブジェクト


*参加オブジェクト*リソース マネージャーの表します[*参加*](transaction-processing-terms.md#ktm-term-enlistment)トランザクションにします。 リソース マネージャーは、トランザクションのイベントに関する通知を受け取ることができます、前に、resource manager を呼び出す必要があります[ **ZwCreateEnlistment** ](https://msdn.microsoft.com/library/windows/hardware/ff566422)トランザクションに参加リストを作成します。

KTM のセットを提供する[参加オブジェクト ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff544270)カーネル モードのリソース マネージャーを呼び出すことができます。 KTM では、ユーザー モード アプリケーションを呼び出すことができるユーザー モード ルーチンのようなセットも提供します。 ユーザー モードのルーチンの詳細については、Microsoft Windows SDK を参照してください。

リソース マネージャーを呼び出すと、KTM は参加リスト オブジェクトを作成**ZwCreateEnlistment** (通常は、トランザクションのクライアント) から、resource manager が受信したトランザクションに参加します。

[TP コンポーネント](understanding-tps-components.md)呼び出せる[ **ZwOpenEnlistment** ](https://msdn.microsoft.com/library/windows/hardware/ff567008)を参加オブジェクトに追加のハンドルを開きます。 ただし、ほとんどの TP の設計に追加の開いているハンドルが必要としません。

リソース マネージャーは、呼び出すことで、参加リストのオブジェクト ハンドルを閉じる[ **ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)します。 KTM がトランザクションを送信する前に、関連付けられているトランザクション オブジェクトがコミットされた最後のハンドルが閉じている場合\_通知\_をトランザクションの参加リストを持つすべてのリソース マネージャーにロールバック通知します。

オペレーティング システムは、最後のハンドルが閉じられ、KTM には、オブジェクトへのすべての参照がリリース後に、オブジェクトを削除します。

 

 




