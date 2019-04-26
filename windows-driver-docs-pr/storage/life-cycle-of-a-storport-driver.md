---
title: Storport ドライバーのライフ サイクル
description: Storport ドライバーのライフ サイクル
ms.assetid: 6b48cf8e-83c3-4403-88fd-1bf1f285aafc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74266fa57d7663c70cbd1e8b0ddec100c1cbdcd8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355628"
---
# <a name="life-cycle-of-a-storport-driver"></a>Storport ドライバーのライフ サイクル


Storport ドライバーのライフ サイクルは、コールバック ルーチンの観点から、Storport ドライバーからミニポート ドライバーに記述できます。 図 1 に示すように、コールバック ルーチンをいくつかの主要グループに分類できます。

![storport の全体的なアーキテクチャを示す図します。](images/storport-1.png)

コールバック ルーチンの各型のいくつかの例は、図 2 に表示されます。 システムが開始され、最初に、ドライバーが読み込まれたとき、ミニポート ドライバーの**DriverEntry**ルーチンが呼び出されます。 このルーチンは、Storport ミニポートのドライバーのエントリ ポイントは、そのコールバック ルーチン、またはコールバックとも呼ばれますに提供するデータ構造体を格納します。 ミニポート ドライバーを呼び出してこのルーチンの最後に、ほぼ[ **StorPortInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff567108)します。 Storport ドライバーを呼び出して、ミニポート コールバック ルーチン[ **HwStorFindAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff557390)、またはの場合は、仮想のミニポート ドライバー [ **VirtualHwStorFindAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff568008). ミニポート ドライバーのルーチンから返された後[ **HwStorInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff557396)ルーチンが呼び出されます。

Storport 取得し、ミニポート ドライバーのサポートされているコントロールの種類を呼び出してその[ **HwStorAdapterControl** ](https://msdn.microsoft.com/library/windows/hardware/ff557365)ルーチン**ScsiQuerySupportedControlTypes**として、パラメーター。

![図 2: storport コールバック ルーチン](images/storport-2.png)

メインの I/O パスは、一連の呼び出しの[ **HwStorBuildIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557369) (仮想のミニポート ドライバーの場合を除く) と[ **HwStorStartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557423). 詳細については、次を参照してください。[同期されていない HwStorBuildIo ルーチン](unsynchronized-hwstorbuildio-routine.md)します。

システムがシャット ダウン、 [ **HwStorStartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557423) 、SRB の SRB の種類を使用して呼び出した\_関数\_シャット ダウンします。 アダプターを削除または無効になっているシステムの実行中、またはシステムが入力するときに休止モード、ときに[ **HwStorAdapterControl** ](https://msdn.microsoft.com/library/windows/hardware/ff557365)を使用して呼び出した**ScsiStopAdapter**をパラメーターとして。 システムがから再開するときに休止モード、 **HwStorAdapterControl**を使用して呼び出した**ScsiRestartAdapter**をパラメーターとして。

 

 




