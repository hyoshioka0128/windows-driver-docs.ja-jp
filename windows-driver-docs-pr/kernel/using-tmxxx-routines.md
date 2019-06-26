---
title: TmXxx ルーチンの使用
description: TmXxx ルーチンの使用
ms.assetid: 8bc763e9-e67c-4810-9901-e5dc1a1cfd0c
keywords:
- カーネル トランザクション マネージャ WDK、TmXxx ルーチン
- KTM WDK、TmXxx ルーチン
- TmXxx ルーチン WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 081b22b2d05539b084c6bdce69632947c7e0645d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358167"
---
# <a name="using-tmxxx-routines"></a>TmXxx ルーチンの使用


ほとんど[KTM ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)の名前付け形式を使用して **Zw*Xxx * * *。 これらのルーチンでは、ハンドル ベースです。 これは、入力または出力パラメーターの少なくとも 1 つは KTM オブジェクトへのハンドルがあります。

KTM は、少数の名前付け形式を使用するルーチンのも用意されています。 **Tm*Xxx * * *。 これらのルーチンでは、ポインター ベースです。 入力または出力パラメーターの少なくとも 1 つは、KTM オブジェクトへのポインターです。

いくつか**Tm * Xxx*** ルーチン重複**Zw * Xxx*** ルーチン。 その他の**Tm * Xxx*** ルーチンがない**Zw * Xxx*** 対応します。

ほとんどの場合、使用する必要があります、 **Zw * Xxx*** ルーチン。 使用する必要がありますが、 **Tm * Xxx*** 次の状況でルーチン。

- Resource manager を使用して、 [ **ResourceManagerNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ptm_rm_notification)コールバック ルーチンは、ハンドルではなく参加オブジェクトへのポインターを提供します。

  参加リストのオブジェクトの登録オブジェクトへのポインターを渡すことができます**Tm * Xxx*** ルーチン。

- (TP) のシステム コンポーネントの処理、トランザクションは、システムのパフォーマンスが非常に長くなる可能性があります KTM に多くの高速呼び出しを実行します。

  この場合、コンポーネントを呼び出すことができます[ **ObReferenceObjectByHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle)各 KTM オブジェクト ハンドルをポインターに変換する、ポインターを保存しへのポインターを渡す**Tm * Xxx*** ルーチン。 この変換に変換する各ハンドルのポインターに内部的に毎回 KTM 必要があるが、 **Zw * Xxx*** ルーチンが呼び出されます。

  呼び出しごとに**ObReferenceObectByHandle** KTM 定義の適切なフラグを含むアクセス マスクを含める必要があります。 KTM の作成し、ルーチンを開くには、これらのフラグをリファレンス ページに説明します。

  いずれかを呼び出すことによって、オブジェクトする必要があります逆参照、コンポーネントの KTM オブジェクトの使用が完了したら、 [ **ObDereferenceObjectDeferDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobjectdeferdelete)または[ **ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject).

  -   使用する必要があります**ObDereferenceObjectDeferDelete**コンポーネント、または他のコンポーネント、ドライバー スタックがスピン ロック、ミュー テックス オブジェクト、または高速なミュー テックスなど、システム指定のロックを保持する場合。

  -   使用することができます**ObDereferenceObject**コンポーネント、ドライバー スタック上にシステム指定のロックが保持していないことを確認します。

  コンポーネントを呼び出す場合、デッドロックが発生する可能性が**ObDereferenceObject** KTM がオブジェクトの名前空間のロックを保持しても可能性がありますので、ロックを保持しているときにします。 また、コンポーネントを呼び出すことができます[ **TmGetTransactionId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-tmgettransactionid)すばやく呼び出すよりも効率的にトランザクションの識別子を取得する[ **ZwQueryInformationTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntqueryinformationtransaction).

- 機能の 1 つがありますが、 **Zw * Xxx*** ルーチンが提供されません。

  具体的には、リソース マネージャーは、次のルーチンを呼び出すことができます。

  -   [**TmEnableCallbacks** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-tmenablecallbacks)コールバック ルーチンによって通知の非同期の配信を有効にします。
  -   [**TmReferenceEnlistmentKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-tmreferenceenlistmentkey)と[ **TmDereferenceEnlistmentKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-tmdereferenceenlistmentkey)インクリメントまたは参加リスト オブジェクトのキーの参照カウントをデクリメントします。
  -   [**TmRequestOutcomeEnlistment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-tmrequestoutcomeenlistment)参加リストの即時コミットまたはロールバック通知を要求します。
  -   [**TmIsTransactionActive** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-tmistransactionactive)をトランザクションがアクティブな状態かどうかを判断します。

 

 




