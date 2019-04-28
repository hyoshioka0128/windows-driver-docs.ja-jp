---
title: BDA ミニドライバーの初期化
description: BDA ミニドライバーの初期化
ms.assetid: 4df2efc6-e666-48d5-9a7b-cbf724c027f0
keywords:
- BDA ミニドライバー WDK AVStream、初期化しています
- BDA ミニドライバー WDK AVStream の初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e754275b219ff69618bff98b713bec62b681d213
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360472"
---
# <a name="initializing-a-bda-minidriver"></a>BDA ミニドライバーの初期化





BDA ミニドライバーは、その他の AVStream ミニドライバーに同様に初期化されます。 BDA ミニドライバーの DriverEntry 関数呼び出し、AVStream [ **KsInitializeDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff562683) BDA ミニドライバーのドライバーのオブジェクトを初期化します。 この呼び出しでは、BDA ミニドライバーはへのポインターを渡します。 を[ **KSDEVICE\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff561691)を含めることができますが、デバイスの特性を指定します。

-   ポインターを[ **KSDEVICE\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff561693) BDA デバイス用のディスパッチ テーブルを含む構造体。 少なくとも BDA ミニドライバーを作成し、デバイスを起動しでこれらのルーチンを指定するルーチンを指定する必要があります、**追加**と**開始**、KSDEVICE のそれぞれのメンバー\_ディスパッチ構造体。 BDA ミニドライバーのルーチンを作成するデバイス クラスのメモリを割り当てへのポインターを参照する必要があります、 [ **KSDEVICE** ](https://msdn.microsoft.com/library/windows/hardware/ff561681) BDA デバイスにこのデバイス クラスの構造体。 BDA ミニドライバーの開始のルーチンでは、レジストリからデバイスに関する情報を取得、デバイスに関する情報を設定、および BDA サポート ライブラリを使用した静的なテンプレートの構造のグループを登録する必要があります。 参照してください[開始 BDA ミニドライバー](starting-a-bda-minidriver.md)詳細についてはします。

-   配列の[ **KSFILTER\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff562553)構造体がこのデバイスでサポートされている個々 のフィルターの種類。 この構造体の型では、指定したフィルター ファクトリによって作成されたフィルターの特性について説明します。 BDA サポート ライブラリを使用しないように、BDA ミニドライバーを作成する場合は、この配列にこの型の構造体のメンバーを指定する必要があります (*Bdasup.lib*) BDA ミニドライバーのプロパティとメソッドを処理するために設定します。 BDA サポート ライブラリを使用するように、BDA ミニドライバーを作成する場合、BDA ミニドライバーは、呼び出す必要があります代わりに、 [ **BdaCreateFilterFactory** ](https://msdn.microsoft.com/library/windows/hardware/ff556438)フィルター ファクトリ記述子 (を追加する関数のサポートKSFILTER\_記述子構造体) デバイス。 参照してください[開始 BDA ミニドライバー](starting-a-bda-minidriver.md)詳細についてはします。

次のコード スニペットでは、フィルター記述子の配列、BDA デバイスでは、および BDA デバイスの記述子にディスパッチ テーブルの例を示します。

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

 

 




