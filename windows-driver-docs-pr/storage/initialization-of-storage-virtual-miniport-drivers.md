---
title: 記憶域仮想ミニポート ドライバーの初期化
description: 記憶域仮想ミニポート ドライバーの初期化
ms.assetid: 35f7bb00-56e0-4535-9f13-9fd33afaa0b5
keywords:
- 記憶域仮想ミニポート ドライバー WDK, 初期化
- ミニポート ドライバー WDK ストレージ
- WDK の記憶域、仮想のミニポート ドライバーの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15c466f5f3ec9a8ecd6fb75931038ef45b6002fa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379104"
---
# <a name="initialization-of-storage-virtual-miniport-drivers"></a>記憶域仮想ミニポート ドライバーの初期化


Storport ミニポート (VMiniport) を仮想ドライバーでは、初期化の 3 つの段階があります。 最初、VMiniport (通常でその[ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチン) 呼び出し[ **StorPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportinitialize)、を表しています[**仮想\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_virtual_hw_initialization_data)構造体。

この構造で、VMiniport はコールバック ルーチンを指す次のフィールドを設定します。

**HwFindAdapter**します。 このルーチンは、初期化の 2 番目のステージが必要です。

**HwInitialize**します。 このルーチンは、初期化の 3 番目のステージが必要です。

**HwInitializeTracing**します。 このルーチンはオプションであり、Storport 仮想ミニポート ドライバーに一意です。

**HwStartIo**します。 このルーチンが必要です。 仮想ミニポート ドライバーで、 **HwStorBuildIo**インターフェイスは、呼び出す前に呼び出されません。 [**HwStorStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio)します。 呼び出しの前にロックがありません。 **HwStorStartIo**します。 仮想ミニポート インターフェイスを通じて公開されている論理ユニットごとの既定のキューの深さは、250 です。

**HwAdapterControl**します。 このルーチンが必要です。

**HwResetBus**します。 このルーチンが必要です。 「バス」の意味は、仮想のミニポート ドライバーの開発者によって定義できます。

**HwProcessServiceRequest**します。 このルーチンはオプションであり、Storport 仮想ミニポート ドライバーに一意です。 このルーチンは、VMiniport、呼び出し元 (ユーザー モード アプリケーションやカーネル モード ドライバー) を更新または VMiniport の代わりに作業を行う呼び出し元を必要とするときに完了する"リバース callback"IRP を受信します。

**HwCompleteServiceIrp**します。 このルーチンはオプションであり、Storport 仮想ミニポート ドライバーに一意です。 ただし、このルーチンは、必要なときに**HwProcessServiceRequest**コールバック ルーチンを指します。 **HwCompleteServiceIrp** VMiniport が保留中になる可能性があるすべてのリバース コールバック Irp を完了できるようにするために、仮想アダプターを削除するときに呼び出されます。

**HwFreeAdapterResources**します。 このルーチンが必要、Storport 仮想ミニポート ドライバーに一意です。 このルーチンは、VMiniport が初期化中に割り当てられているすべてのリソースを解放するために、仮想アダプターを削除するときに呼び出されます。

**HwCleanupTracing**します。 このルーチンはオプションであり、Storport 仮想ミニポート ドライバーに一意です。 ただし、このルーチンは、必要なときに**HwInitializeTracing**コールバック ルーチンを指します。

仮想のミニポート ドライバーも、同じ構造で以下の設定する必要があります。

**HwInitializationDataSize** = **sizeof**(仮想\_HW\_初期化\_データ)。

**AdapterInterfaceType** = **内部**します。

Storport 仮想ミニポート ドライバーは、必要に応じて、他のフィールドを設定します。 使用されていないフィールドは、0 に設定する必要があります。

すべてのロックを保持することがなくとパッシブ\_レベル、仮想のミニポート ドライバー呼び出し[ **StorPortInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportinitialize)へのポインターを[**仮想\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_virtual_hw_initialization_data)構造体し、し、返される状態を確認します。 Storport ドライバーは、この構造体の情報のコピーを保持し、ミニポート ドライバーでは後にこの構造体が保持されない必要があります**StorPortInitialize**を返します。

[**仮想\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_virtual_hw_initialization_data) Storport.h に表示されます。

 

 




