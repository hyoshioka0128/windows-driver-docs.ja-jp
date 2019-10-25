---
title: Storport ドライバーのライフ サイクル
description: Storport ドライバーのライフ サイクル
ms.assetid: 6b48cf8e-83c3-4403-88fd-1bf1f285aafc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77430baf44731f93741bdba1c493ede07f42a662
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841622"
---
# <a name="life-cycle-of-a-storport-driver"></a>Storport ドライバーのライフ サイクル


Storport ドライバーのライフサイクルは、コールバックルーチンの観点から、Storport ドライバーのミニポートドライバーに記述できます。 コールバックルーチンは、図1に示すように、いくつかのメイングループに分類できます。

![storport アーキテクチャ全体を示す図](images/storport-1.png)

図2に、コールバックルーチンの各種類の例をいくつか示します。 システムが起動し、ドライバーが最初に読み込まれると、ミニポートドライバーの**Driverentry**ルーチンが呼び出されます。 このルーチンは、Storport にミニポートドライバーのエントリポイント (コールバックルーチンまたはコールバックとも呼ばれます) を提供するデータ構造を入力します。 このルーチンの終了間際に、ミニポートドライバーは[**Storportinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportinitialize)を呼び出します。 次に、Storport ドライバーは、ミニポートコールバックルーチン[**HwStorFindAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)を呼び出します。または、仮想ミニポートドライバー [**VirtualHwStorFindAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-virtual_hw_find_adapter)の場合はを呼び出します。 そのルーチンからが返されると、ミニポートドライバーの[**HwStorInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_initialize)ルーチンが呼び出されます。

Storport は、パラメーターとして**ScsiQuerySupportedControlTypes**を指定して[**HwStorAdapterControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_adapter_control)ルーチンを呼び出すことによって、ミニポートドライバーでサポートされているコントロールの種類を取得します。

![図 2: storport コールバックルーチン](images/storport-2.png)

メイン i/o パスは、 [**HwStorBuildIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_buildio)への一連の呼び出し (仮想ミニポートドライバーの場合を除く) と[**HwStorStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio)で構成されます。 詳細については、「[同期 HwStorBuildIo ルーチン](unsynchronized-hwstorbuildio-routine.md)」を参照してください。

システムがシャットダウンされると、 [**HwStorStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio)は SRB 型の\_SRB を使用して呼び出され、\_シャットダウンします。 システムの実行中、またはシステムの休止モードに入っているときに、アダプターが削除または無効にされた場合、 [**HwStorAdapterControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_adapter_control)は**ScsiStopAdapter**を使用してパラメーターとして呼び出されます。 システムが休止モードから再開されると、 **HwStorAdapterControl**が**ScsiRestartAdapter**と共にパラメーターとして呼び出されます。

 

 




