---
title: BDA フィルター プロパティの変更
description: BDA フィルター プロパティの変更
ms.assetid: 1833864a-5759-437c-ba60-0b38602d9e41
keywords:
- プロパティ設定 WDK BDA, フィルタープロパティの変更
- フィルタープロパティの変更 WDK BDA
- メソッドは、WDK BDA、filter プロパティの変更を設定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aafcd613c246846eb545362018b125a6c0e22caa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844737"
---
# <a name="changing-bda-filter-properties"></a>BDA フィルター プロパティの変更





メディアブロードキャストを表示するアプリケーションの複数のインスタンスをシステム上で同時に実行できるため、フィルターの複数のインスタンスに対応するように BDA ミニドライバーを作成する必要があります。 各フィルターインスタンスには、さまざまな情報を含めることができます。 たとえば、チューナーフィルターの1つのインスタンスには、チャネル5へのチューニング要求を含めることができますが、別のインスタンスには、チャネル8へのチューニング要求を含めることができます。 コントロールがあるインスタンスから別のインスタンスに遷移するとき、BDA ミニドライバーは基になるチューニングデバイスに対して、リソースの構成方法を変更するように指示する必要があります。 BDA ミニドライバーは、BdaChangeSync メソッドに設定されている[Ksk Methodsetid\_](https://docs.microsoft.com/windows-hardware/drivers/stream/ksmethodsetid-bdachangesync)のメソッド要求を処理し、ミニドライバーのフィルターインスタンスでプロパティ要求のリストを調整します。

KSK METHODSETID\_BdaChangeSync メソッドセットの主な目的は、フィルターの基になるミニドライバーがミニドライバーの device オブジェクトからリソースを取得して解放できるトリガーポイントを提供することです。 ミニドライバーは、これらのトリガーポイントを、停止状態との間のフィルターの遷移で調整する必要があります。 たとえば、フィルターが停止状態の場合、ミニドライバーは新しいリソースをフィルターに割り当てる必要がありますが、ネットワークプロバイダーが BDA トポロジの変更をコミットするように指定するたびに、リソースを取得することはできません。 その後、フィルターが停止状態から移行すると、ミニドライバーは、基になるデバイスからそれらのリソースを取得しようとする必要があります。

一方、フィルターが既にアクティブになっている場合、ミニドライバーは、ネットワークプロバイダーが BDA トポロジの変更をコミットするように指定するたびに、基になるデバイスから新しいリソースを取得しようとする必要があります。 アクティブにできるのは、フィルターの1つのインスタンスだけです。実行中の状態では、同時に同じリソースを保持できます。 フィルターが停止状態に遷移すると、そのピンに割り当てられたリソースも含め、すべてのリソースが解放されます。これにより、実行中の状態に遷移する別のフィルターグラフでリソースを使用できるようになります。

通常、BDA ミニドライバーのフィルターオブジェクトは、KSK METHODSETID\_BdaChangeSync メソッドセットのメソッドのメソッドをインターセプトして提供します。 たとえば、ミニドライバーには、フィルターの変更を開始、確認、コミットし、フィルターの変更状態を取得するためのメソッドが用意されています。 また、次のミニドライバーで提供されるメソッドは、ミニドライバーが以前に BDA サポートライブラリに登録した構造の変更を同期するために、対応する BDA サポートライブラリ関数を呼び出す必要があります。

-   開始-変更メソッドは[**Bdastartchanges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdastartchanges)関数を呼び出します。

-   Check changes メソッドは、 [**BdaCheckChanges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdacheckchanges)関数を呼び出します。

-   Commit-changes メソッドは、 [**BdaCommitChanges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdacommitchanges)関数を呼び出します。

-   [**BdaGetChangeState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdagetchangestate)メソッドは、この関数を呼び出します。

次のコードスニペットは、内部メソッドを使用して、KSK METHODSETID\_BdaChangeSync メソッドに設定されたメソッド要求をインターセプトする方法を示しています。

```cpp
//
//  BDA Change Sync Method Set
//
//  Defines the dispatch routines for the filter level
//  Change Sync methods
//
DEFINE_KSMETHOD_TABLE(BdaChangeSyncMethods)
{
    DEFINE_KSMETHOD_ITEM_BDA_START_CHANGES(
        CFilter::StartChanges,
        NULL
        ),
    DEFINE_KSMETHOD_ITEM_BDA_CHECK_CHANGES(
        CFilter::CheckChanges,
        NULL
        ),
    DEFINE_KSMETHOD_ITEM_BDA_COMMIT_CHANGES(
        CFilter::CommitChanges,
        NULL
        ),
    DEFINE_KSMETHOD_ITEM_BDA_GET_CHANGE_STATE(
        CFilter::GetChangeState,
        NULL
        )
};
```

次のコードスニペットは、ミニドライバーが**Bdastartchanges**サポート関数を呼び出して新しい bda トポロジ変更の設定を開始した後に、bda ミニドライバーの内部の開始変更メソッドが保留中のリソースの変更をリセットする方法を示しています。

```cpp
//
// StartChanges ()
//
//    Puts the filter into change state.  All changes to BDA topology
//    and properties changed after this will be in effect only after
//    CommitChanges.
//
NTSTATUS
CFilter::
StartChanges(
    IN PIRP         pIrp,
    IN PKSMETHOD    pKSMethod,
    OPTIONAL PVOID  pvIgnored
    )
{
    NTSTATUS        Status = STATUS_SUCCESS;
    CFilter *       pFilter;

    ASSERT( pIrp);
    ASSERT( pKSMethod);

    // Obtain a "this" pointer for the method.
    //
    // Because this function is called directly from the property 
    // dispatch table, must get pointer to the underlying object.
    //
    pFilter = FilterFromIRP( pIrp);
    ASSERT( pFilter);
    if (!pFilter)
    {
        Status = STATUS_INVALID_PARAMETER;
        goto errExit;
    }

    //  Reset any pending BDA topology changes.
    //
    Status = BdaStartChanges( pIrp);
    if (!NT_SUCCESS( Status))
    {
        goto errExit;
    }

    //  Reset any pending resource changes.
    //
    pFilter->m_NewTunerResource = pFilter->m_CurTunerResource;
    pFilter->m_BdaChangeState = BDA_CHANGES_COMPLETE;

errExit:
    return Status;
}
```

 

 




