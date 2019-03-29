---
title: C28167
description: 警告 C28167 関数は IRQL を変更し、終了前に、IRQL は復元されません。 変更を反映するようにマーク付けする必要があります。 または IRQL が復元する必要があります。
ms.assetid: 289bb3c9-f9b2-4e7f-a406-22e365e5316a
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28167
ms.openlocfilehash: 790a0e6c241e043c31994e6d4ed12dc3c30131fd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570151"
---
# <a name="c28167"></a>C28167


C28167 を警告します。関数は IRQL を変更し、終了前に、IRQL は復元されません。 変更を反映するようにマーク付けする必要があります。 または IRQL が復元する必要があります。

この警告は、次の条件に該当することを示します。

-   関数は、位置、ドライバーが実行中の IRQL を変更します。

-   少なくとも 1 つのパス、関数の終了を復元しません、IRQL ドライバーは、関数のエントリで実行されていた元の IRQL を関数があります。

この警告は、関数、IRQL の注釈が必要ですが、1 つが存在しない場合に発生します。

この警告を回避するために、ドライバーが正しく、初期の IRQL の値を保存し、IRQL の変更が意図しない場合は、関数の終了時、同じ IRQL の値を復元する必要があります。

意図的に、IRQL を関数のエントリをドライバーが実行中の IRQL とは異なる値に変更する関数をこの動作を示すために注釈を付ける必要があります。 たとえば、使用する、  **\_IRQL\_発生\_**(*irql*)、関数が位置 IRQL からの IRQL を変更することを示すの注釈関数呼び出されました。 保存し、IRQL の値を復元して対応する注釈を適用 (**\_IRQL\_保存\_**、  **\_IRQL\_の復元\_**). 注釈には、この警告が抑制されます。 詳細については、次を参照してください。[ドライバーの IRQL の注釈](irql-annotations-for-drivers.md)します。 IRQL を誤って変更関数を修正する必要があります。

 

 





