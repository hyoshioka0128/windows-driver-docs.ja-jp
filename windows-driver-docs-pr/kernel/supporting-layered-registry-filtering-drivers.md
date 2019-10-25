---
title: 複数層レジストリ フィルター ドライバーのサポート
description: 複数層レジストリ フィルター ドライバーのサポート
ms.assetid: 5adeecdb-c26e-4502-87b4-bfb02a4aaba8
keywords:
- レジストリのフィルター選択 WDK カーネル、階層化
- レジストリフィルタリングドライバー WDK カーネル、階層化
- 階層化レジストリフィルタードライバー WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 543ffbbcafb7ddfad7e48c9b11d0bdc750d8a86e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836215"
---
# <a name="supporting-layered-registry-filtering-drivers"></a>複数層レジストリ フィルター ドライバーのサポート


Windows Vista 以降のバージョンのオペレーティングシステムでは、レジストリフィルタリングドライバーの階層化されたスタックがサポートされています。 スタック内の各ドライバーは、 [*Registrycallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ex_callback_function)ルーチンを登録することによって、レジストリ操作のフィルター処理に参加できます。 各レジストリフィルタードライバーには*高度*が割り当てられ、ドライバーは各高度につき1つの*registrycallback*ルーチンのみを登録できます。 ドライバーが[**Cmregisterの ex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallbackex)を呼び出すと、ドライバーの高度が指定されます。 高度の詳細については、「[ミニフィルタードライバーの読み込み順序グループと高度](https://docs.microsoft.com/windows-hardware/drivers/ifs/load-order-groups-and-altitudes-for-minifilter-drivers)」を参照してください。

スレッドがレジストリ呼び出しを行うと、configuration manager は、すべてのドライバーが呼び出されるか、または*Registrycallback*ルーチンによって状態値が返されるまで、各*registrycallback*ルーチンを順番に呼び出します。成功した[NT\_](using-ntstatus-values.md)(*状態*) は**FALSE**になります。 したがって、上位レベルのドライバーがレジストリ操作をブロックまたは変更した場合、下位レベルのドライバーは呼び出されません。 (ドライバーが別のレジストリ機能を呼び出して操作を変更した場合、構成マネージャーはフィルタースタックの一番上では再起動しません)。

Windows Vista より前に記述されたレジストリフィルタリングドライバーは、Windows Vista のフィルタースタックの先頭付近に、 [**Cmregistercallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallback)を呼び出す順序で挿入されます。

 

 




