---
title: BDA フィルターの構成
description: BDA フィルターの構成
ms.assetid: 4af9efc3-8073-4111-9ad0-8b2fba4d1545
keywords:
- メソッドは WDK BDA、フィルター構成を設定します
- プロパティ設定 WDK BDA, フィルター構成
- KSMETHODSETID_BdaDeviceConfiguration
- フィルターの構成 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50f57c7916ccc552c658772faf54374420a1bb37
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844709"
---
# <a name="configuring-a-bda-filter"></a>BDA フィルターの構成





BDA ミニドライバーは、現在のフィルターグラフのミニドライバーに対してフィルターインスタンスを構成するように設定された、 [Ksk Methodsetid\_](https://docs.microsoft.com/windows-hardware/drivers/stream/ksmethodsetid-bdadeviceconfiguration)のメソッド要求を処理します。

次のコードスニペットでは、KSMETHODSETID\_BdaDeviceConfiguration メソッドセットの2つのメソッドが、BDA サポートライブラリに直接ディスパッチされます。残りのメソッドは、bda にディスパッチする前に、BDA によって最初に受け取られます。サポートライブラリ。

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

KSK メソッド\_BDA\_CREATE\_TOPOLOGY メソッド要求は、ミニドライバーの CFilter:: CreateTopology メソッドを呼び出します。 このメソッドは、BDA サポートライブラリ関数[**BdaMethodCreateTopology**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdamethodcreatetopology)を呼び出して、フィルターピン間のトポロジを作成します。 この関数は、実際には、他のプロパティセットのフィルターの既知の接続を反映するトポロジ構造をリング3で作成します。 ミニドライバーが特定の pin の種類に接続するときにハードウェアに特別な命令を送信する必要がある場合、前のコードスニペットに示すように、BDA ミニドライバーは KSK メソッド\_\_BDA をインターセプトし、\_トポロジメソッド要求を作成する必要があります。たとえば、BDA デバイスがハードウェア demultiplexing 化を実行し、1つの入力ピンから任意の数の出力ピン重ねを作成したとします。

 

 




