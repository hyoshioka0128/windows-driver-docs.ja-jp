---
title: トランザクション マネージャー オブジェクト
description: トランザクション マネージャー オブジェクト
ms.assetid: af53cda4-e2ab-47df-9311-a4da2a2ee08d
keywords:
- ログ ストリーム WDK KTM を作成します。
- 仮想のクロック値 WDK の KTM をトランザクション マネージャー オブジェクト
- カーネル トランザクション マネージャ WDK、トランザクション マネージャー
- オブジェクトの WDK KTM をトランザクション マネージャー
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f617d8724a5e38a389f54510802ba5084b7955c0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573734"
---
# <a name="transaction-manager-objects"></a>トランザクション マネージャー オブジェクト


主な目的、*トランザクション マネージャー オブジェクト*作成および管理するには、 [Common Log File System](using-common-log-file-system.md) KTM をトランザクションのレコードの状態情報を使用する (CLFS) ログ ストリーム。

トランザクション マネージャーのオブジェクトにも含まれています、[仮想クロック値](using-virtual-clock-values.md)KTM を維持し、オブジェクトのログ ストリームのシーケンスの情報を使用します。

KTM のセットを提供する[トランザクション マネージャー オブジェクト ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff564807)カーネル モード[TP コンポーネント](understanding-tps-components.md)呼び出すことができます。 KTM では、ユーザー モード アプリケーションを呼び出すことができるユーザー モード ルーチンのようなセットも提供します。 ユーザー モードのルーチンの詳細については、Microsoft Windows SDK を参照してください。

リソース マネージャーを呼び出すと、KTM がトランザクション マネージャー オブジェクトを作成します[ **ZwCreateTransactionManager**](https://msdn.microsoft.com/library/windows/hardware/ff566430)します。 通常、TP では、各リソース マネージャーは、トランザクション マネージャー オブジェクトを作成します。 ただし、いくつかのリソース マネージャーが 1 つのトランザクション マネージャー オブジェクトを共有 TP を設計することもできます。

TP コンポーネントは、呼び出すことによって、既存のトランザクション マネージャー オブジェクトへの追加のハンドルを開くことができます[ **ZwOpenTransactionManager**](https://msdn.microsoft.com/library/windows/hardware/ff567035)します。 たとえば、TP に 1 つのトランザクション マネージャー オブジェクトを共有しているいくつかのリソース マネージャーがある場合は、一方が resource manager を呼び出す**ZwCreateTransactionManager**し、他のリソース マネージャーをオブジェクトの GUID を渡しますように呼び出すことによって**ZwOpenTransactionManager**します。

リソース マネージャーは、呼び出すことでトランザクション マネージャー オブジェクトへのハンドルを閉じる[ **ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)します。

オペレーティング システムは、最後のハンドルが閉じられ、KTM には、オブジェクトへのすべての参照がリリース後に、オブジェクトを削除します。

 

 




