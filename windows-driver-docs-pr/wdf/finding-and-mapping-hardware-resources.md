---
title: ハードウェア リソースの検索とマッピング
description: このトピックでは、カーネル モード ドライバー フレームワーク (KMDF) ドライバーまたはバージョン 2 でユーザー モード ドライバー フレームワーク (UMDF) ドライバーがその EvtDevicePrepareHardware コールバックで受信した翻訳済みのメモリ リソース (CmResourceTypeMemory) をマップする方法について説明します関数。
ms.assetid: 9D65D70C-FFF1-4663-8701-221C5443C425
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fb22e5d332435ae6159fdfb3d6cca96fb2d97eb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391354"
---
# <a name="finding-and-mapping-hardware-resources"></a>ハードウェア リソースの検索とマッピング


このトピックでは、カーネル モード ドライバー フレームワーク (KMDF) ドライバーまたはユーザー モード ドライバー フレームワーク (UMDF) ドライバーのバージョン 2 での翻訳済みのメモリ リソースをマップする方法について説明します (**CmResourceTypeMemory**) そので受信した[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)コールバック関数。

1.x UMDF ドライバーでは、この種類のリソースを受け取ることもその[ **IPnpCallbackHardware2::OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/hh439734)メソッド。 詳細については、次を参照してください。 [UMDF 1.x ドライバー内のハードウェア リソースのマッピングの検索と](finding-and-mapping-hardware-resources-in-umdf-1-x-drivers.md)します。

ドライバーを受け取る[生、翻訳した](raw-and-translated-resources.md)のバージョンで、デバイスのリソースのリスト内のハードウェア リソースの[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)コールバック関数。 ドライバーがドライバーのフレームワークになるまでの有効なリソースの一覧を保存できます[ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)コールバック関数。

ドライバーの呼び出しでは通常、 [ **WdfCmResourceListGetCount** ](https://msdn.microsoft.com/library/windows/hardware/ff545687)からその[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)にコールバック関数翻訳されたリソースの一覧、および呼び出すリソースの記述子の数を決定[ **WdfCmResourceListGetDescriptor** ](https://msdn.microsoft.com/library/windows/hardware/ff545688)レジスタのメモリ マップ I/O ポートを識別するためにループ内で、および割り込みです。

ドライバーでの翻訳済みのメモリ リソースが割り当てられている場合 (**CmResourceTypeMemory**)、それを使用するデバイスの登録にアクセスできるアドレスに、物理アドレスをマッピングする必要があります。

KMDF ドライバーは呼び出し[ **MmMapIoSpace** ](https://msdn.microsoft.com/library/windows/hardware/ff554618)ページングされないシステム領域に、特定の物理アドレスの範囲をマップします。 使用して、 [ **HAL ライブラリ ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff546644)に読み取りし、書き込みを登録します。

UMDF ドライバーは呼び出し[ **WdfDeviceMapIoSpace** ](https://msdn.microsoft.com/library/windows/hardware/dn265605)擬似のベース アドレスと組み合わせて使用できる物理アドレスにマップする[WDF 登録/ポート アクセス関数](https://msdn.microsoft.com/library/windows/hardware/dn265662)レジスタ、およびポートを読み書きする方法。

ドライバーを呼び出して、リソースの割り当てを解除[ **MmUnmapIoSpace** ](https://msdn.microsoft.com/library/windows/hardware/ff556387)または[ **WdfDeviceUnmapIoSpace** ](https://msdn.microsoft.com/library/windows/hardware/dn265610)からその[ *EvtDeviceReleaseHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540890)コールバック関数。

I/O 領域内のリソースをマップする必要はありません (**CmResourceTypePort**、 **CmResourceTypeInterrupt**、 **CmResourceTypeDma**)。

UMDF ドライバーを呼び出す場合[ **WdfDeviceMapIoSpace**](https://msdn.microsoft.com/library/windows/hardware/dn265605)を設定する必要があります、 **UmdfDirectHardwareAccess** INF ディレクティブを**AllowDirectHardwareAccess**.

例については、ドライバーを検索し、メモリ マップト マップ リソースを登録する方法を示しますが、次を参照してください。[読み取りと書き込みをデバイスの登録](reading-and-writing-to-device-registers.md)します。

 

 





