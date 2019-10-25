---
title: ミニポートドライバールーチン内の同期されたアクセス
description: ミニポートドライバーが全二重モードで実行されている場合や、SRBs の処理が同期されていない場合でも、同期アクセスが必要になることがあります。
ms.assetid: a1bc3bff-b109-4a52-8466-48a0be7611b7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ee0f723f270112655b821948ddc9c7529b77942
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844452"
---
# <a name="synchronized-access-within-miniport-driver-routines"></a>ミニポートドライバールーチン内の同期されたアクセス


## <span id="ddk_synchronized_access_within_unsynchronized_miniport_driver_routines"></span><span id="DDK_SYNCHRONIZED_ACCESS_WITHIN_UNSYNCHRONIZED_MINIPORT_DRIVER_ROUTINES"></span>


ミニポートドライバーが全二重モードで実行されている場合、または[**HwStorBuildIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_buildio)ルーチンで SRBs の非同期処理が行われている場合でも、デバイス拡張機能への同期アクセスが必要になる場合があります。 Storport ドライバーによって提供されるサポートルーチンのライブラリには、 [**StorPortSynchronizeAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportsynchronizeaccess)が含まれています。これは、ミニポートドライバーがデバイス拡張機能などの重要なデータ構造へのアクセスを同期できるようにするルーチンです。

ミニポートドライバーは**StorPortSynchronizeAccess**を呼び出すときに、コールバックルーチンへのポインターを使用してルーチンを提供する必要があります。 コールバックルーチンには、ホストバスアダプターの割り込みハンドラーと同期する必要がある SRB の処理の一部が含まれています。 パフォーマンスを向上させるには、コールバックルーチンを実行するできるだけ短い時間でドライバーを記述します。

 

 




