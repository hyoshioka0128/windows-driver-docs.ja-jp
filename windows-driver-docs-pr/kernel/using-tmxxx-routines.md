---
title: TmXxx ルーチンの使用
description: TmXxx ルーチンの使用
ms.assetid: 8bc763e9-e67c-4810-9901-e5dc1a1cfd0c
keywords:
- カーネルトランザクションマネージャー WDK、TmXxx ルーチン
- KTM WDK、TmXxx ルーチン
- TmXxx ルーチン WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbac18629f721e7121cbc4231df8199eeb34f37c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838325"
---
# <a name="using-tmxxx-routines"></a>TmXxx ルーチンの使用


ほとんどの[KTM ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)では、**Zw*Xxx * * * という名前付け形式を使用します。 これらのルーチンはハンドルベースです。 つまり、少なくとも1つの入力パラメーターまたは出力パラメーターが、KTM オブジェクトへのハンドルです。

また、KTM は、**Tm*Xxx * * * という名前付け形式を使用する、より少ない数のルーチンも提供します。 これらのルーチンは、ポインターに基づいています。 少なくとも1つの入力パラメーターまたは出力パラメーターが、KTM オブジェクトへのポインターです。

一部の**Tm * xxx*** ルーチンで**Zw * xxx*** ルーチンが重複しています。 その他の**Tm * xxx*** ルーチンには、同等の**Zw * xxx*** がありません。

ほとんどの場合、 **Zw * Xxx*** ルーチンを使用する必要があります。 ただし、次のような状況では、 **Tm * Xxx*** ルーチンを使用する必要があります。

- リソースマネージャーは[**ResourceManagerNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ptm_rm_notification)コールバックルーチンを使用します。これにより、ハンドルではなく、参加リストオブジェクトへのポインターが提供されます。

  参加リストオブジェクトのポインターを、登録オブジェクトの**Tm * Xxx*** ルーチンに渡すことができます。

- トランザクション処理システム (TPS) コンポーネントは、KTM に対して多くの高速呼び出しを実行するため、システムのパフォーマンスが低下する可能性があります。

  この場合、コンポーネントは、 [**Obreferenceobjectbyhandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)を呼び出して各 KTM オブジェクトハンドルをポインターに変換し、ポインターを保存してから、そのポインターを**Tm * Xxx*** ルーチンに渡すことができます。 この変換により、 **Zw * Xxx*** ルーチンが呼び出されるたびに、KTM によって各ハンドルが内部的にポインターに変換される必要がなくなります。

  **Obreferenceobて Byhandle**を呼び出すたびに、適切な KTM 定義フラグを含むアクセスマスクを含める必要があります。 これらのフラグは、KTM の作成ルーチンとオープンルーチンのリファレンスページで説明されています。

  コンポーネントで KTM オブジェクトの使用が完了したら、 [**ObDereferenceObjectDeferDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobjectdeferdelete)または[**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)を呼び出してオブジェクトを逆参照する必要があります。

  -   コンポーネントまたはドライバースタック内の他のコンポーネントが、スピンロック、ミューテックスオブジェクト、高速ミューテックスなどのシステム指定のロックを保持している場合は、 **ObDereferenceObjectDeferDelete**を使用する必要があります。

  -   ドライバースタック上のコンポーネントがシステム指定のロックを保持していないことが確実な場合は、 **ObDereferenceObject**を使用できます。

  コンポーネントがロックを保持しながら**ObDereferenceObject**を呼び出した場合にデッドロックが発生する可能性があります。これは、KTM がオブジェクトの名前空間のロックを保持している場合もあるためです。 また、コンポーネントは、 [**Tmgettransactionid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-tmgettransactionid)を呼び出して、 [**Zwqueryinformationtransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntqueryinformationtransaction)を呼び出すよりも効率的にトランザクションの識別子を取得することができます。

- **Zw * Xxx*** ルーチンによって提供されない機能が必要です。

  具体的には、リソースマネージャーは次のルーチンを呼び出すことができます。

  -   [**Tmenablecallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-tmenablecallbacks)は、コールバックルーチンによる通知の非同期配信を可能にします。
  -   [**TmReferenceEnlistmentKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-tmreferenceenlistmentkey)と[**TmDereferenceEnlistmentKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-tmdereferenceenlistmentkey)は、参加オブジェクトのキー参照カウントをインクリメントまたはデクリメントします。
  -   [**TmRequestOutcomeEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-tmrequestoutcomeenlistment)は、参加リストの即時コミットまたはロールバック通知を要求します。
  -   [**TmIsTransactionActive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-tmistransactionactive)は、トランザクションがアクティブな状態であるかどうかを判断します。

 

 




