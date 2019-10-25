---
title: APC の無効化
description: APC の無効化
ms.assetid: 0578df31-1467-4bad-ba62-081d61278deb
keywords:
- 非同期プロシージャ呼び出し WDK カーネル
- Apc WDK カーネル
- Apc の無効化
- 重要なリージョン WDK カーネル
- 保護されたリージョンの WDK カーネル
- 現在の IRQLs の発生
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61b7a2a72f97f2cb2731d34d2cceb54d2fe3ae44
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836905"
---
# <a name="disabling-apcs"></a>APC の無効化


システムには、現在のスレッドの Apc を無効にするための3つのメカニズムが用意されています。

-   **重要なリージョン。** スレッドがクリティカル領域内にある場合、そのユーザーの Apc と通常のカーネル Apc は実行されません。 特殊なカーネル Apc は引き続き実行されます。 これらの APC 型の詳細については、「 [apc の型](types-of-apcs.md)」を参照してください。

-   **保護されたリージョン。** スレッドが保護された領域内にある場合、その Apc は実行されません。

-   **現在の IRQL を APC\_レベル以上に上げています。** IRQL &gt;= APC\_LEVEL で実行中のスレッドは、すべての Apc を無効にして実行されます。

これらの設定は現在のスレッドに適用され、他のスレッドの動作には影響しないことに注意してください。

一部のドライバーサポートルーチンは、特定の種類の Apc を無効にして呼び出す必要があります。 たとえば、エグゼクティブリソース ( [**ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)など) を取得するルーチンは、通常のカーネル apc を無効にして呼び出す必要があります。 その他のルーチンは、特定の種類の Apc が有効になっている状態で呼び出す必要があります。 たとえば、i/o 完了ルーチン ( [**Iovolumedevicetodosname**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iovolumedevicetodosname)など) に依存するルーチンは、特別なカーネル apc が有効になっている状態で呼び出す必要があります。 各ルーチンのドキュメントでは、ルーチンに APC 実行の状態に関する特定の制限があるかどうかを指定します。

ドライバーは、適切なルーチンを呼び出すことによって、重大または保護されたリージョンに明示的に入力できます。 詳細については、「[クリティカルなリージョンと保護](critical-regions-and-guarded-regions.md)されたリージョン」を参照してください。 ドライバーは、 [**Keraiseirql**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql)を呼び出すことにより、現在の IRQL を APC\_レベルに明示的に上げることもできます。 その後、 [**kelower irql**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql)を呼び出すことによって、ドライバーは irql を元の値に下げる必要があります。 保護された領域の使用は、現在の IRQL の発生と減少よりも高速ですが、保護された領域は Windows Server 2003 以降のバージョンの Windows でのみ使用できます。

次の mutex 操作は、重大または保護されたリージョンを入力したり、そのままにしたり、現在の IRQL を上げたり下げたりする場合と同じ効果があります。

-   ミューテックスオブジェクトを保持すると、その所有者が暗黙的にクリティカル領域内に配置されます。

-   保護されたミューテックスを保持すると、保護されたリージョン内にホルダーが暗黙的に配置されます。

-   高速ミューテックスを保持すると、現在の IRQL が APC\_レベルに暗黙的に発生します。

Mutex オブジェクトの詳細については、「 [Mutex オブジェクト](mutex-objects.md)」を参照してください。 高速ミューテックスと保護されたミューテックスの詳細については、「[高速ミューテックスと保護](fast-mutexes-and-guarded-mutexes.md)されたミューテックス」を参照してください。

 

 




