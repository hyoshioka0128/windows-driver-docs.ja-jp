---
title: 記憶域仮想ミニポート ドライバーの初期化
description: 記憶域仮想ミニポート ドライバーの初期化
ms.assetid: 35f7bb00-56e0-4535-9f13-9fd33afaa0b5
keywords:
- ストレージ仮想ミニポートドライバー WDK、初期化
- ミニポートドライバー WDK ストレージ
- WDK ストレージの初期化、仮想ミニポートドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7eb3fbe593f9858838a53e0ec76884638fdc85e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845375"
---
# <a name="initialization-of-storage-virtual-miniport-drivers"></a>記憶域仮想ミニポート ドライバーの初期化


Storport 仮想ミニポート (VMiniport ポート) ドライバーには、初期化の3つの段階があります。 1つ目の方法では、VMiniport ポート (通常は[*Driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチン) が[**storportinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportinitialize)を呼び出します。これにより、[**仮想\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/ns-storport-_virtual_hw_initialization_data)構造が参照されます。

この構造体では、VMiniport ポートは、コールバックルーチンを指す次のフィールドを設定します。

**HwFindAdapter**。 このルーチンは、初期化の2番目の段階で必要になります。

**HwInitialize**。 このルーチンは、初期化の3番目の段階で必要になります。

**HwInitializeTracing**。 このルーチンは省略可能であり、Storport 仮想ミニポートドライバーに固有のものです。

**HwStartIo**。 このルーチンは必須です。 仮想ミニポートドライバーでは、 **HwStorBuildIo**インターフェイスはを呼び出す前に呼び出されません。 [**HwStorStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio)。 を呼び出す前にロックが保持されません。 **HwStorStartIo**。 仮想ミニポートインターフェイスを介して公開される各論理ユニットの既定のキューの深さは250です。

**HwAdapterControl**。 このルーチンは必須です。

**HwResetBus**。 このルーチンは必須です。 "Bus" の意味は、仮想ミニポートドライバーの開発者が定義できます。

**HwProcessServiceRequest**。 このルーチンは省略可能であり、Storport 仮想ミニポートドライバーに固有のものです。 このルーチンは、"逆コールバック" IRP を受信します。この IRP は、VMiniport ポートが呼び出し元 (ユーザーモードアプリケーションやカーネルモードドライバーなど) を更新したときに完了します。または、呼び出し元が VMiniport ポートに代わって何らかの処理を行う必要がある場合にも完了します。

**HwCompleteServiceIrp**。 このルーチンは省略可能であり、Storport 仮想ミニポートドライバーに固有のものです。 ただし、 **HwProcessServiceRequest**がコールバックルーチンをポイントする場合は、このルーチンが必要です。 **HwCompleteServiceIrp**は、仮想アダプターが削除されるときに呼び出されます。これにより、vminiport ポートは、保留中の可能性のある逆コールバック irp を完了できるようになります。

**HwFreeAdapterResources**。 このルーチンは必須であり、Storport 仮想ミニポートドライバーに固有のものです。 このルーチンは、仮想アダプターが削除されるときに呼び出されます。これにより、初期化中に割り当てられたすべてのリソースを VMiniport ポートで解放できるようになります。

**HwCleanupTracing**。 このルーチンは省略可能であり、Storport 仮想ミニポートドライバーに固有のものです。 ただし、 **HwInitializeTracing**がコールバックルーチンをポイントする場合は、このルーチンが必要です。

また、仮想ミニポートドライバーでは、次の設定も同じ構造にする必要があります。

**Hwinitializationdatasize** = **sizeof**(仮想\_HW\_初期化\_データ)。

**AdapterInterfaceType** = **内部**。

Storport 仮想ミニポートドライバーは、必要に応じて他のフィールドを設定します。 未使用のフィールドは0に設定する必要があります。

ロックを保持し、パッシブ\_レベルでは、仮想ミニポートドライバーは、[**仮想\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/ns-storport-_virtual_hw_initialization_data)構造へのポインターを使用して[**storportinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportinitialize)を呼び出し、次の状態を確認します。結果. Storport ドライバーは、この構造の情報の独自のコピーを保持します。また、 **Storportinitialize**が返された後に、ミニポートドライバーはこの構造を保持する必要がありません。

[**VIRTUAL\_HW\_の初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/ns-storport-_virtual_hw_initialization_data)が Storport に表示されます。

 

 




