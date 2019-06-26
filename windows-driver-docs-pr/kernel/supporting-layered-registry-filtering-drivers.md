---
title: 複数層レジストリ フィルター ドライバーのサポート
description: 複数層レジストリ フィルター ドライバーのサポート
ms.assetid: 5adeecdb-c26e-4502-87b4-bfb02a4aaba8
keywords:
- レジストリの呼び出しの WDK カーネルをフィルター処理には、階層化
- レジストリのドライバー WDK カーネル、階層型のフィルター処理
- フィルター ドライバー WDK カーネル レジストリを階層化
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd9c451a34d73a2225a2a40a5711bfa31a82a377
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385110"
---
# <a name="supporting-layered-registry-filtering-drivers"></a>複数層レジストリ フィルター ドライバーのサポート


Windows Vista およびそれ以降のオペレーティング システム バージョンは、レジストリのドライバーをフィルター処理の階層化のスタックをサポートします。 各ドライバー スタックでは、レジストリの操作を登録することでフィルター処理に参加できる、 [ *RegistryCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ex_callback_function)ルーチン。 各レジストリのドライバーをフィルタ リングが割り当てられている、*高度*、ドライバーが 1 つだけを登録および*RegistryCallback*ごとの高度の日常的な。 ドライバーを呼び出すと[ **CmRegisterCallbackEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-cmregistercallbackex)ドライバーがその高度を指定します。 高度の詳細については、次を参照してください。[ロード順序グループとミニフィルター ドライバーの高度](https://docs.microsoft.com/windows-hardware/drivers/ifs/load-order-groups-and-altitudes-for-minifilter-drivers)します。

スレッドを呼び出すレジストリと、configuration manager を呼び出し各*RegistryCallback*ルーチン低いものまで、最高の高度からの順序で、すべてのドライバーが呼び出されるまで、 *RegistryCallback*ルーチンは、対象の状態値を返します[NT\_成功](using-ntstatus-values.md)(*状態*) と等しい**FALSE**します。 そのためより高度なドライバーは、ブロックか、レジストリの操作を変更する場合は、下位レベルのドライバーは呼び出されません。 (ドライバーは、異なるレジストリ関数を呼び出すことによって、操作を変更する場合、configuration manager を再起動しませんフィルター スタックの上部にある。)

呼び出しの順序で、Windows Vista フィルター スタックの上部にある Windows Vista より前に記述された、そのため、高度が割り当てられていないフィルター ドライバーのレジストリが挿入される[ **CmRegisterCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-cmregistercallback).

 

 




