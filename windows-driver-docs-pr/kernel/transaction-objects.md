---
title: トランザクション オブジェクト
description: トランザクション オブジェクト
ms.assetid: 124105bd-70be-49b1-8ea4-af6ba1f3cf16
keywords:
- トランザクション WDK KTM、オブジェクト
- トランザクション WDK KTM
- トランザクションクライアント WDK KTM、トランザクションの作成
- カーネルトランザクションマネージャー WDK、トランザクション
- KTM WDK、トランザクション
- トランザクションオブジェクト WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 642eb1da820e1bbcdaa207bedd72874bd824eab6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838382"
---
# <a name="transaction-objects"></a>トランザクション オブジェクト


*トランザクションオブジェクト*はトランザクションを表します。 トランザクションクライアントはトランザクションを作成し、何らかの処理を実行します。また、トランザクションをコミットするか、ロールバックします。

KTM には、カーネルモードのトランザクションクライアントが呼び出すことができる一連の[トランザクションオブジェクトルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)が用意されています。 また、KTM は、ユーザーモードアプリケーションが呼び出すことができる同様のユーザーモードルーチンのセットも提供します。 ユーザーモードルーチンの詳細については、「Microsoft Windows SDK」を参照してください。

クライアントが[**Zwcreatetransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransaction)を呼び出すときに、KTM はトランザクションオブジェクトを作成します。 クライアントは、 [**Zwcommittransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction)または[**ZwRollbackTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbacktransaction)を呼び出して、トランザクションをコミットまたはロールバックできます。

[Tp コンポーネント](understanding-tps-components.md)は、 [**zwopentransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopentransaction)を呼び出して、トランザクションオブジェクトに対する追加ハンドルを開くことができます。

クライアントは[**Zwclose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)を呼び出して、トランザクションオブジェクトに対するハンドルを閉じます。 トランザクションオブジェクトがコミットされる前に最後のハンドルを閉じた場合、KTM はトランザクションを送信して、トランザクションの参加リストを持つすべてのリソースマネージャーに\_ロールバック通知を通知\_ます。

最後のハンドルが閉じられ、KTM によってオブジェクトへのすべての参照が解放された後、オペレーティングシステムによってオブジェクトが削除されます。

 

 




