---
title: KTM オブジェクト
description: KTM オブジェクト
ms.assetid: 927a417b-35f5-49b8-85f3-7e6b1f5c0225
keywords:
- カーネル トランザクション マネージャ WDK、オブジェクト
- KTM WDK、オブジェクト
- WDK の KTM オブジェクト
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 153a1e71943b3ef96f0be3e4636554d003dec5b5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531405"
---
# <a name="ktm-objects"></a>KTM オブジェクト


カーネル トランザクション マネージャー (KTM) では、次の 4 つのオブジェクトの種類を定義します。

-   [トランザクション マネージャー オブジェクト](transaction-manager-objects.md)、KTM がメモリ常駐型情報の管理に使用する、 [*ログ ストリーム*](transaction-processing-terms.md#ktm-term-log-stream)の[*トランザクション処理システム* ](transaction-processing-terms.md#ktm-term-transaction-processing-system) (TPS)。

-   [リソース マネージャー オブジェクト](resource-manager-objects.md)、表します、 [*リソース マネージャー* ](transaction-processing-terms.md#ktm-term-resource-manager) TP 内。

-   [トランザクション オブジェクト](transaction-objects.md)、トランザクションを表すを[*トランザクション クライアント*](transaction-processing-terms.md#ktm-term-transactional-client)を作成します。

-   [参加リストのオブジェクト](enlistment-objects.md)、表します[*参加リスト*](transaction-processing-terms.md#ktm-term-enlistment)トランザクションとリソース マネージャー間の接続を提供します。

次の 4 つのオブジェクトの種類すべてでは、次の特徴があります。

-   オブジェクトを作成し、オブジェクトのハンドルを取得する[TP コンポーネント](understanding-tps-components.md)呼び出すことができます、*作成*ルーチン。

-   既存のオブジェクトに追加のオブジェクトのハンドルを取得する TP コンポーネントを呼び出すことができます、*開く*ルーチン。

-   オブジェクトに関する情報を取得する TP コンポーネントを呼び出すことができます、*クエリ*ルーチン。

-   TP コンポーネントの呼び出し、オブジェクトのハンドルを閉じる[ **ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)します。

KTM では、各オブジェクトに識別子の GUID を割り当てます。 この識別子は GUID とも呼ばれますが、トランザクション オブジェクト、*作業 (UOW) 識別子の単位*クライアントを指定できます。 TP コンポーネントでは、オブジェクトを追跡するために、識別子の Guid を使用できます。 オブジェクトを作成する TP コンポーネントは、後者のコンポーネントが、オブジェクトを識別するハンドルを開けるように、別のコンポーネントに、オブジェクトの識別子 GUID を渡すことができます。

KTM を使用する任意の TP コンポーネントを呼び出すことができます[ **ZwEnumerateTransactionObject** ](https://msdn.microsoft.com/library/windows/hardware/ff566450) KTM を列挙するオブジェクトが、ほとんどのコンポーネントは、このルーチンを呼び出す必要はありません。

このセクションには、次のトピックが含まれています。

[トランザクション マネージャー オブジェクト](transaction-manager-objects.md)

[Resource Manager オブジェクト](resource-manager-objects.md)

[トランザクション オブジェクト](transaction-objects.md)

[参加リストのオブジェクト](enlistment-objects.md)

 

 




