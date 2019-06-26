---
title: リソース マネージャー オブジェクト
description: リソース マネージャー オブジェクト
ms.assetid: b44f2035-ee9f-453b-b12d-89ca36a8b280
keywords:
- WDK KTM、オブジェクトのリソース マネージャー
- リソース マネージャー WDK KTM
- WDK KTM、ルーチンのリソース マネージャー
- カーネル トランザクション マネージャ WDK、リソース マネージャー
- KTM WDK、リソース マネージャー
- リソース マネージャーは、WDK KTM をオブジェクトします。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7a99a4897b5eb225b524af70fe8057c464ae107
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373410"
---
# <a name="resource-manager-objects"></a>リソース マネージャー オブジェクト


*リソース マネージャー オブジェクト*リソース マネージャーを表します。 各リソース マネージャーを呼び出す必要があります[ **ZwCreateResourceManager** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreateresourcemanager) KTM を登録します。

KTM のセットを提供する[リソース マネージャー オブジェクト ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)カーネル モードのリソース マネージャーを呼び出すことができます。 KTM では、ユーザー モード アプリケーションを呼び出すことができるユーザー モード ルーチンのようなセットも提供します。 ユーザー モードのルーチンの詳細については、Microsoft Windows SDK を参照してください。

リソース マネージャーを呼び出すと、KTM がリソース マネージャー オブジェクトを作成します**ZwCreateResourceManager**します。

[TP コンポーネント](understanding-tps-components.md)呼び出すことができます[ **ZwOpenResourceManager** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntopenresourcemanager)を resource manager のオブジェクトに追加のハンドルを開きます。 ただし、ほとんどの TP の設計に追加の開いているハンドルが必要としません。

リソース マネージャーは、呼び出すことで resource manager のオブジェクトへのハンドルを閉じる[ **ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)します。 かどうかの最後のハンドルは閉じられ、KTM がトランザクションを送信する場合は、リソース マネージャーがまだコミットされていないトランザクションに参加リストを使用して、\_通知\_はトランザクションのすべてのリソース マネージャーにロールバック通知これらの参加リストに関連付けられました。

オペレーティング システムは、最後のハンドルが閉じられ、KTM には、オブジェクトへのすべての参照がリリース後に、オブジェクトを削除します。

 

 




