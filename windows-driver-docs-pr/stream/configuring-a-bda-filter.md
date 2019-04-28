---
title: BDA フィルターの構成
description: BDA フィルターの構成
ms.assetid: 4af9efc3-8073-4111-9ad0-8b2fba4d1545
keywords:
- メソッドは、WDK BDA、フィルターの構成を設定します。
- プロパティは、WDK BDA、フィルターの構成を設定します。
- KSMETHODSETID_BdaDeviceConfiguration
- WDK BDA フィルターの構成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67271ef4282cf2e8634f16dc35bafe50db68bfd6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374188"
---
# <a name="configuring-a-bda-filter"></a>BDA フィルターの構成





BDA ミニドライバーのメソッドの要求の処理、 [KSMETHODSETID\_BdaDeviceConfiguration](https://msdn.microsoft.com/library/windows/hardware/ff563404)フィルターの現在のグラフでミニドライバーのフィルターのインスタンスを構成する方法を設定します。

2 つ、KSMETHODSETID のメソッドの次のコード スニペットで\_BDA サポート ライブラリに直接ディスパッチ BdaDeviceConfiguration メソッドのセットと残りのメソッドにディスパッチする前にインターセプト BDA ミニドライバーで最初BDA サポート ライブラリ。

```cpp
//
//  BDA Device Configuration Method Set
//
//  Defines the dispatch routines for the filter level
//  topology configuration methods
//
DEFINE_KSMETHOD_TABLE(BdaDeviceConfigurationMethods)
{
    DEFINE_KSMETHOD_ITEM_BDA_CREATE_PIN_FACTORY(
        BdaMethodCreatePin,
        NULL
        ),
    DEFINE_KSMETHOD_ITEM_BDA_DELETE_PIN_FACTORY(
        BdaMethodDeletePin,
        NULL
        ),
    DEFINE_KSMETHOD_ITEM_BDA_CREATE_TOPOLOGY(
        CFilter::CreateTopology,
        NULL
        )
};
/*
** CreateTopology()
**
** Keeps track of topology association between input and output pins
**
*/
NTSTATUS
CFilter::
CreateTopology(
    IN PIRP         pIrp,
    IN PKSMETHOD    pKSMethod,
    PVOID           pvIgnored
    )
{
    NTSTATUS            Status = STATUS_SUCCESS;
    CFilter *           pFilter;
    ULONG               ulPinType;
    PKSFILTER           pKSFilter;

    ASSERT( pIrp);
    ASSERT( pKSMethod);

    //  Obtain a "this" pointer for the method.
    //
    //  Because this function is called directly from the property 
    //  dispatch table, get pointer to the underlying object.
    //
    pFilter = FilterFromIRP( pIrp);
    ASSERT( pFilter);
    if (!pFilter)
    {
        Status = STATUS_INVALID_PARAMETER;
        goto errExit;
    }

    //  Let the BDA support library create the standard topology.
    //  It will also validate the method, instance count, etc.
    //
    Status = BdaMethodCreateTopology( pIrp, pKSMethod, pvIgnored);
    if (Status != STATUS_SUCCESS)
    {
        goto errExit;
    }

    //  This is where the filter can keep track of associated pins.
    //
errExit:
    return Status;
}
```

KSMETHOD\_BDA\_作成\_トポロジ メソッド要求は、ミニドライバーの CFilter::CreateTopology メソッドを呼び出します。 このメソッドは、BDA サポート ライブラリ関数を呼び出す[ **BdaMethodCreateTopology** ](https://msdn.microsoft.com/library/windows/hardware/ff556471)フィルター ピンの間のトポロジを作成します。 実際には、この関数は、その他のプロパティ セットのフィルターの既知の接続を反映するリング 3 でトポロジ構造を作成します。 BDA ミニドライバーは、KSMETHOD をインターセプトする必要があります\_BDA\_作成\_メソッド要求のかどうかそのミニドライバー送信する必要が特別な手順については、ハードウェアに接続するときに特定の前のコード スニペットに示すトポロジ入力ピンが 1 つからオフに変換し暗証番号 (pin) の種類--BDA デバイスがハードウェアの多重を実行し、任意の数の出力ピンを作成する場合などです。

 

 




