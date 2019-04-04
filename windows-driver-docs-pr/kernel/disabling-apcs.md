---
title: Apc を無効にします。
description: Apc を無効にします。
ms.assetid: 0578df31-1467-4bad-ba62-081d61278deb
keywords:
- 非同期プロシージャ呼び出しの WDK カーネル
- Apc WDK カーネル
- Apc を無効にします。
- クリティカル領域 WDK カーネル
- 保護された領域の WDK カーネル
- 現在の Irql を発生させる
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5ccf8f8be7cfbed04a95732a4101a05d5f923b6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548615"
---
# <a name="disabling-apcs"></a>Apc を無効にします。


システムでは、現在のスレッドの Apc を無効にする 3 つのメカニズムを提供します。

-   **クリティカル領域。** スレッドがクリティカル領域内にある場合は、そのユーザーの Apc と通常のカーネル Apc は実行されません。 特別なカーネル Apc は引き続き実行されます。 これらの APC 種類の詳細については、[型の Apc](types-of-apcs.md)を参照してください。

-   **保護された領域。** スレッドが保護された領域の内側にある場合は、その Apc のいずれも実行されます。

-   **APC を現在の IRQL を発生させる\_レベルまたはそれ以降。** IRQL でを実行しているスレッド&gt;APC を =\_レベルが無効になっているすべての Apc を実行します。

これらの設定が、現在のスレッドに適用され、他のスレッドの動作には影響しないことに注意してください。

特定の種類の Apc を無効になっているとは、いくつかのドライバー サポート ルーチンを呼び出す必要があります。 Executive のリソースを取得するルーチンなど (など[ **ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)) 呼び出す通常カーネル Apc を無効になっている必要があります。 特定の種類の Apc が有効になっていると、その他のルーチンを呼び出す必要があります。 たとえば、任意のルーチン、I/O 完了ルーチンに依存している (など[ **IoVolumeDeviceToDosName**](https://msdn.microsoft.com/library/windows/hardware/ff550422)) 特別なカーネル Apc が有効になっているで呼び出す必要があります。 各ルーチンは、ドキュメントでは、ルーチンが、APC 実行の状態に関する特定の制約がかどうかを指定します。

ドライバーは、適切なルーチンを呼び出すことによって、重要なまたは保護された領域を明示的に入力できます。 詳細については、[クリティカル領域および領域の保護された](critical-regions-and-guarded-regions.md)を参照してください。 ドライバーは APC を現在の IRQL を上げることができますも明示的に\_呼び出してレベル[ **KeRaiseIrql**](https://msdn.microsoft.com/library/windows/hardware/ff553079)します。 ドライバーを呼び出して元の値に IRQL を下げる必要があります、その後[ **KeLowerIrql**](https://msdn.microsoft.com/library/windows/hardware/ff552968)します。 現在の IRQL では、値の増減により高速では保護された領域の使用が、保護された領域は Windows Server 2003 以降のバージョンの Windows で利用できますのみ。

ミュー テックスの次の操作では、入力または重大または保護された領域を離れることまたは発生または現在の IRQL を下げると同じ効果があります。

-   ミュー テックス オブジェクトを暗黙的に保持するいると、クリティカル領域内で、所有者が配置されます。

-   保護されたミュー テックスを暗黙的に保持している保護された領域内で、所有者を配置します。

-   APC を現在の IRQL を発生させる、高速なミュー テックスを暗黙的に保持している\_レベル。

ミュー テックス オブジェクトの詳細については、[ミュー テックス オブジェクト](mutex-objects.md)を参照してください。 高速で保護されたミュー テックスの詳細については、[高速なミュー テックスと保護されたミュー テックス](fast-mutexes-and-guarded-mutexes.md)を参照してください。

 

 




