---
title: システム電源状態変更の防止
description: システム電源状態変更の防止
ms.assetid: a744dfe7-d756-45c3-8fdf-7a403f6cde36
keywords:
- システム電源の状態 WDK カーネル、変更の防止
- 状態遷移 WDK 電源管理
- PoRegisterSystemState
- PoSetSystemState
- PoUnregisterSystemState
- 作業状態 WDK の電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3779d3bc717cbcb91c7befe5c75fe20c0c2c868f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827630"
---
# <a name="preventing-system-power-state-changes"></a>システム電源状態変更の防止





ドライバーはシステムの電源ポリシーを直接設定することはできませんが、電源マネージャーには次の3つのルーチンが用意されています。これにより、ドライバーが動作状態からシステムの移行を妨げることがあります。 [**Posetsystemstate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-posetsystemstate)、 [**PoRegisterSystemState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-poregistersystemstate)、 [**PoUnregisterSystemState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pounregistersystemstate)。

ドライバーは、 **PoRegisterSystemState**または**Posetsystemstate**を呼び出すことにより、ユーザーが存在すること、またはドライバーがシステムまたは表示を使用する必要があることを電源マネージャーに通知できます。

**PoRegisterSystemState**を使用すると、ドライバーは連続したビジー状態を登録できます。 ドライバーは、後で設定を変更できるハンドルを返します。 状態の登録が有効になっている限り、電源マネージャーはシステムをスリープ状態にしません。 ドライバーは、 **Pounregistersystemstate**を呼び出すことによって状態の登録を取り消します。

**Posetsystemstate**を使用すると、ドライバーは同じ条件 (ユーザーが存在し、システムが必要、表示が必要) をパワーマネージャーに通知しますが、この設定は連続していません。 指定した条件に関連付けられているアイドル状態のカウントダウンを再起動した場合の効果があります。

これらのルーチンを使用すると、ドライバーは多くのことを forestall することができますが、すべてではなく、動作状態から遷移します。 電源が切断された場合、またはユーザーが明示的にシャットダウンを要求した場合、電源マネージャーは常にシステムをシャットダウンします。

 

 




