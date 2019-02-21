---
title: 階層型のレジストリのドライバーをフィルター処理をサポートしています。
description: 階層型のレジストリのドライバーをフィルター処理をサポートしています。
ms.assetid: 5adeecdb-c26e-4502-87b4-bfb02a4aaba8
keywords:
- レジストリの呼び出しの WDK カーネルをフィルター処理には、階層化
- レジストリのドライバー WDK カーネル、階層型のフィルター処理
- フィルター ドライバー WDK カーネル レジストリを階層化
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10f6a5f86e4ba8807194fbce1748c5943aec5fee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532314"
---
# <a name="supporting-layered-registry-filtering-drivers"></a>階層型のレジストリのドライバーをフィルター処理をサポートしています。


Windows Vista およびそれ以降のオペレーティング システム バージョンは、レジストリのドライバーをフィルター処理の階層化のスタックをサポートします。 各ドライバー スタックでは、レジストリの操作を登録することでフィルター処理に参加できる、 [ *RegistryCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff560903)ルーチン。 各レジストリのドライバーをフィルタ リングが割り当てられている、*高度*、ドライバーが 1 つだけを登録および*RegistryCallback*ごとの高度の日常的な。 ドライバーを呼び出すと[ **CmRegisterCallbackEx**](https://msdn.microsoft.com/library/windows/hardware/ff541921)ドライバーがその高度を指定します。 高度の詳細については、次を参照してください。[ロード順序グループとミニフィルター ドライバーの高度](https://msdn.microsoft.com/library/windows/hardware/ff549689)します。

スレッドを呼び出すレジストリと、configuration manager を呼び出し各*RegistryCallback*ルーチン低いものまで、最高の高度からの順序で、すべてのドライバーが呼び出されるまで、 *RegistryCallback*ルーチンは、対象の状態値を返します[NT\_成功](using-ntstatus-values.md)(*状態*) と等しい**FALSE**します。 そのためより高度なドライバーは、ブロックか、レジストリの操作を変更する場合は、下位レベルのドライバーは呼び出されません。 (ドライバーは、異なるレジストリ関数を呼び出すことによって、操作を変更する場合、configuration manager を再起動しませんフィルター スタックの上部にある。)

呼び出しの順序で、Windows Vista フィルター スタックの上部にある Windows Vista より前に記述された、そのため、高度が割り当てられていないフィルター ドライバーのレジストリが挿入される[ **CmRegisterCallback**](https://msdn.microsoft.com/library/windows/hardware/ff541918).

 

 




