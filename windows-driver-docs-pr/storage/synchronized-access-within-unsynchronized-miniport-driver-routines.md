---
title: ミニポート ドライバー ルーチン内の同期アクセス
description: ミニポート ドライバーでは、全二重モードで実行またはされる Srb の処理が同期されていない、ときにも同期アクセスが必要ですがあります。
ms.assetid: a1bc3bff-b109-4a52-8466-48a0be7611b7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4226c5e572f252f5facc095e8150f50d46c6411b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578486"
---
# <a name="synchronized-access-within-miniport-driver-routines"></a>ミニポート ドライバー ルーチン内の同期アクセス


## <span id="ddk_synchronized_access_within_unsynchronized_miniport_driver_routines"></span><span id="DDK_SYNCHRONIZED_ACCESS_WITHIN_UNSYNCHRONIZED_MINIPORT_DRIVER_ROUTINES"></span>


でもミニポート ドライバー全二重モードで実行またはとでされる Srb の非同期処理を行って、 [ **HwStorBuildIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557369) 、日常的な必要がありますが、デバイスの拡張機能への同期アクセスします。 Storport ドライバーによって提供されるサポート ルーチンのライブラリに含まれる[ **StorPortSynchronizeAccess**](https://msdn.microsoft.com/library/windows/hardware/ff567511)、ミニポート ドライバーの重要なデータへのアクセスを同期するを許可するルーチンがこのような構造体として、デバイスの拡張機能。

ミニポート ドライバーを呼び出すと**StorPortSynchronizeAccess**、コールバック ルーチンへのポインターとルーチンを指定する必要があります。 コールバック ルーチンには、ホスト バス アダプターの割り込みハンドラーと同期する必要があります SRB の処理の一部が含まれています。 パフォーマンスの向上のためには、コールバック ルーチンを実行することにかかる時間は、ドライバーを記述します。

 

 




