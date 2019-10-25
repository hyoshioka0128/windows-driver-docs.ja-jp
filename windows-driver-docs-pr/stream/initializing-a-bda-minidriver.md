---
title: BDA ミニドライバーの初期化
description: BDA ミニドライバーの初期化
ms.assetid: 4df2efc6-e666-48d5-9a7b-cbf724c027f0
keywords:
- BDA ミニドライバー WDK AVStream、初期化
- BDA ミニドライバー WDK AVStream を初期化しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a67f7a6c9825066cc189b9b1bebe026d9798c4f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845574"
---
# <a name="initializing-a-bda-minidriver"></a>BDA ミニドライバーの初期化





BDA ミニドライバーは、他の AVStream ミニドライバーと同様に初期化されます。 BDA ミニドライバーの DriverEntry 関数は、AVStream [**Ksinitializedriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedriver)関数を呼び出して、bda ミニドライバーの driver オブジェクトを初期化します。 この呼び出しでは、BDA ミニドライバーは、次のようなデバイスの特性を指定する[**Ksk デバイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice_descriptor)構造体へのポインターを渡します。

-   BDA デバイスのディスパッチテーブルを含む[**Ksk デバイス\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice_dispatch)構造体へのポインター。 少なくとも、BDA ミニドライバーは、デバイスを作成して起動するルーチンを提供する必要があります。また、これらのルーチンは、KSK デバイス\_ディスパッチ構造体の **[追加]** および **[開始]** メンバーで指定します。 BDA ミニドライバーの create ルーチンは、デバイスクラスにメモリを割り当て、BDA デバイスの[**Ksk デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice)構造へのポインターをこのデバイスクラスに参照する必要があります。 BDA ミニドライバーの開始ルーチンは、レジストリからデバイスに関する情報を取得し、デバイスに関する情報を設定してから、静的なテンプレート構造のグループを BDA サポートライブラリに登録する必要があります。 詳細について[は、「BDA ミニドライバーの開始](starting-a-bda-minidriver.md)」を参照してください。

-   このデバイスでサポートされている個々のフィルターの種類に対して、 [**Ksk フィルター\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)構造体の配列。 この構造体型は、特定のフィルターファクトリによって作成されたフィルターの特性を記述します。 Bda サポートライブラリ (*Bdasup*) を使用して bda ミニドライバーのプロパティとメソッドのセットを処理しないように、bda ミニドライバーを作成する場合は、この配列にこの型の構造体のメンバーを指定する必要があります。 Bda サポートライブラリを使用するように BDA ミニドライバーを作成する場合は、代わりに、BDA ミニドライバーが[**Bdacreatefilterfactory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdacreatefilterfactory)サポート関数を呼び出して、フィルターファクトリ記述子 (ksk フィルター\_記述子構造) をドライブ. 詳細について[は、「BDA ミニドライバーの開始](starting-a-bda-minidriver.md)」を参照してください。

次のコードスニペットは、フィルター記述子の配列、BDA デバイスのディスパッチテーブル、および BDA デバイスの記述子の例を示しています。

```cpp
//
//  Array containing descriptors for all filter factories
//  available on the device.
//
//  Note!  Only used when dynamic topology is not used (that is, 
//         only when filters and pins are fixed). Typically, this 
//         is when the network provider is not present.
//
DEFINE_KSFILTER_DESCRIPTOR_TABLE(FilterDescriptors)
{
    &TemplateTunerFilterDescriptor
};
//
//  Device Dispatch Table
//
//  Lists the dispatch routines for the major events related to 
//  the underlying device.
//
extern
const
KSDEVICE_DISPATCH
DeviceDispatch =
{
    CDevice::Create,    // Add
    CDevice::Start,     // Start
    NULL,               // PostStart
    NULL,               // QueryStop
    NULL,               // CancelStop
    NULL,               // Stop
    NULL,               // QueryRemove
    NULL,               // CancelRemove
    NULL,               // Remove
    NULL,               // QueryCapabilities
    NULL,               // SurpriseRemoval
    NULL,               // QueryPower
    NULL                // SetPower
};
//
//  Device Descriptor
//
//  Brings together the data structures that define the device and
//  the initial filter factories that can be created on it.
//  Note that because template topology structures are specific 
//  to BDA, the device descriptor does not include them.
//  Note also that if BDA dynamic topology is used, the device 
//  descriptor does not specify a list of filter factory descriptors.
//  If BDA dynamic topology is used, the BDA minidriver calls 
//  BdaCreateFilterFactory to add filter factory descriptors. 
extern
const
KSDEVICE_DESCRIPTOR
DeviceDescriptor =
{
    &DeviceDispatch,    // Dispatch
#ifdef DYNAMIC_TOPOLOGY // network provider is present
    0,    // FilterDescriptorsCount
    NULL, // FilterDescriptors
#else     // network provider is not present
    SIZEOF_ARRAY( FilterDescriptors), // FilterDescriptorsCount
    FilterDescriptors                 // FilterDescriptors
#endif // DYNAMIC_TOPOLOGY
```

 

 




