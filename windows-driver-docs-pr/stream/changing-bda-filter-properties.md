---
title: BDA フィルター プロパティの変更
description: BDA フィルター プロパティの変更
ms.assetid: 1833864a-5759-437c-ba60-0b38602d9e41
keywords:
- プロパティは、WDK BDA、フィルター プロパティの変更を設定します。
- WDK BDA フィルターのプロパティの変更
- メソッドは、WDK BDA、フィルター プロパティの変更を設定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5f2d456e8e19154c4d5d1c3012defd46343c9c1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351852"
---
# <a name="changing-bda-filter-properties"></a>BDA フィルター プロパティの変更





メディア放送のビューがシステムに同時に実行できるアプリケーションの複数のインスタンス、フィルターの複数のインスタンスに対応する BDA ミニドライバーを作成する必要があります。 各フィルターのインスタンスは、さまざまな情報を含めることができます。 たとえば、チューナーのフィルターの 1 つのインスタンスは、別のインスタンスにチャネル 8 にチューニングする要求を含めることができます、5、チャネルを調整できる要求を含めることができます。 コントロールが遷移する 1 つのインスタンスから、BDA ミニドライバーにリソースを構成する方法を変更する場合は、基になるチューニング デバイスを指定する必要があります。 BDA ミニドライバーのメソッドの要求の処理、 [KSMETHODSETID\_BdaChangeSync](https://msdn.microsoft.com/library/windows/hardware/ff563403)プロパティの一覧を調整する設定メソッドでは、ミニドライバーのフィルターのインスタンスを 1 つ上に要求します。

主な目的、KSMETHODSETID\_BdaChangeSync メソッドのセットがフィルターの基になるミニドライバーを取得し、ミニドライバーのデバイス オブジェクトからリソースを解放する位置のトリガー ポイントを提供することです。 ミニドライバーは、フィルターの移行と停止の状態の間でこれらのトリガー ポイントを調整する必要があります。 たとえば、フィルターが停止状態にある場合、ミニドライバーする必要があります、フィルターに新しいリソースを割り当てるがネットワーク プロバイダーを指定 BDA トポロジの変更をコミットするたびに、これらのリソースを取得できません。 フィルターは、その後その停止状態から遷移をミニドライバーは、基になるデバイスからそれらのリソースを取得しようとする必要があります。

その一方で、フィルターが既にアクティブである場合、ミニドライバーは、BDA トポロジの変更をコミットするネットワーク プロバイダーが指定されるたびに、基になるデバイスからの新しいリソースを取得しようとします。 フィルターの 1 つだけのインスタンスは実行中の状態と、同じリソースを保持する特定の時点でアクティブ--できます。 停止状態に遷移する場合、フィルター、ときに、そのため、リソースが別のフィルター グラフが実行中の状態に遷移に使用できるように、そのピンのいずれかに割り当てられたこれらのリソースを含むすべてのリソースを解放する必要があります。

通常は、BDA ミニドライバーのフィルター オブジェクトを傍受し、KSMETHODSETID のメソッドのメソッドを提供\_BdaChangeSync メソッドのセット。 たとえば、ミニドライバーは、以降、検査、およびフィルターの変更をコミットし、フィルターの変更状態を取得するメソッドを提供します。 さらに、次のミニドライバーが指定したメソッド呼び出す必要があります BDA サポートは、対応するライブラリ関数、ミニドライバーは BDA サポート ライブラリに既に登録された構造に変更を同期します。

-   変更の開始メソッドの呼び出し、 [ **BdaStartChanges** ](https://msdn.microsoft.com/library/windows/hardware/ff556507)関数。

-   チェック変更メソッドの呼び出し、 [ **BdaCheckChanges** ](https://msdn.microsoft.com/library/windows/hardware/ff556433)関数。

-   変更をコミット メソッドの呼び出し、 [ **BdaCommitChanges** ](https://msdn.microsoft.com/library/windows/hardware/ff556435)関数。

-   Get 変更状態メソッドの呼び出し、 [ **BdaGetChangeState** ](https://msdn.microsoft.com/library/windows/hardware/ff556458)関数。

次のコード スニペットは、KSMETHODSETID のメソッドの要求をインターセプトする方法を示しています。\_BdaChangeSync メソッドの内部メソッドを使用して設定します。

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

次のコード スニペットは、ミニドライバーの呼び出し後、BDA ミニドライバーの内部変更開始メソッドが保留中のリソースの変更をリセットする方法を示しています、 **BdaStartChanges**新しい BDA トポロジの設定を開始する関数のサポート変更:

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

 

 




