---
title: KTM オブジェクト
description: KTM オブジェクト
ms.assetid: 927a417b-35f5-49b8-85f3-7e6b1f5c0225
keywords:
- カーネルトランザクションマネージャー WDK、オブジェクト
- KTM WDK、オブジェクト
- オブジェクト WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a30606c8755b437cbff2bb5b57e2a3ccd8ddf7c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838557"
---
# <a name="ktm-objects"></a>KTM オブジェクト


カーネルトランザクションマネージャー (KTM) では、次の4種類のオブジェクトが定義されています。

-   トランザクション[マネージャーオブジェクト](transaction-manager-objects.md)。 KTM は、[*トランザクション処理システム*](transaction-processing-terms.md#ktm-term-transaction-processing-system)(TPS) の[*ログストリーム*](transaction-processing-terms.md#ktm-term-log-stream)に関するメモリ常駐情報を保持するために使用されます。

-   [リソースマネージャーオブジェクト](resource-manager-objects.md)。 tp 内の[*リソースマネージャー*](transaction-processing-terms.md#ktm-term-resource-manager)を表します。

-   [トランザクションオブジェクト](transaction-objects.md)は、トランザクション[*クライアント*](transaction-processing-terms.md#ktm-term-transactional-client)によって作成されるトランザクションを表します。

-   [参加オブジェクト](enlistment-objects.md)。トランザクションとリソースマネージャー間の接続を提供する参加[*リスト*](transaction-processing-terms.md#ktm-term-enlistment)を表します。

これらの4種類のオブジェクトには、次の特性があります。

-   オブジェクトを作成し、オブジェクトハンドルを取得するには、 [tp コンポーネント](understanding-tps-components.md)が*create*ルーチンを呼び出すことができます。

-   既存のオブジェクトに対する追加のオブジェクトハンドルを取得するために、TP コンポーネントは*オープン*ルーチンを呼び出すことができます。

-   オブジェクトに関する情報を取得するために、TP コンポーネントは*クエリ*ルーチンを呼び出すことができます。

-   オブジェクトハンドルを閉じるには、TPS コンポーネントが[**Zwclose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)を呼び出します。

KTM は、識別子の GUID を各オブジェクトに割り当てます。 トランザクションオブジェクトの場合、この識別子の GUID は、クライアントが指定できる*作業単位 (UOW) 識別子*とも呼ばれます。 TP コンポーネントでは、識別子 Guid を使用してオブジェクトを追跡できます。 オブジェクトを作成する TP コンポーネントは、オブジェクトの識別子 GUID を別のコンポーネントに渡すことができます。これにより、後者のコンポーネントがオブジェクトへのハンドルを開けるようになります。

KTM を使用する TP コンポーネントは、 [**ZwEnumerateTransactionObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntenumeratetransactionobject)を呼び出して、ktm オブジェクトを列挙できますが、ほとんどのコンポーネントはこのルーチンを呼び出す必要はありません。

このセクションは、次のトピックで構成されています。

[トランザクションマネージャーオブジェクト](transaction-manager-objects.md)

[Resource Manager オブジェクト](resource-manager-objects.md)

[トランザクションオブジェクト](transaction-objects.md)

[参加リストオブジェクト](enlistment-objects.md)

 

 




