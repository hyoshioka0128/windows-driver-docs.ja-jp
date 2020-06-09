---
ms.assetid: E109BD80-F9CB-4F1F-A6FD-1142E27EC6AD
title: Windows ドライバーの概要
description: Windows ドライバーでは、Windows 10X と Windows デスクトップ両方で実行されるドライバーを 1 つ作成できます。
ms.date: 04/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 2640310a12a2d111fb1d617e4aa9c5a7413c5fa5
ms.sourcegitcommit: 609c5731b2db4c17b9959082c4621c001e012db1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2020
ms.locfileid: "84223513"
---
# <a name="getting-started-with-windows-drivers"></a>Windows ドライバーの概要

ある時点の Windows 10 (バージョン 2004) から、Windows 上で実行されるドライバーは、"*Windows ドライバー*" と "*Windows デスクトップ ドライバー*" のいずれかに分類されます。 

Windows ドライバーは、Windows 10X と Windows 10 デスクトップ エディションを含む、Windows 10 のすべてのバリエーションで実行されます。  Windows デスクトップ ドライバーが実行されるのは、Windows 10 デスクトップ エディション "*のみ*" です。  

"*Windows ドライバー*" の分類が拡張され、現在の "*ユニバーサル ドライバー*" の分類に取って代わります。 

このページでは、Windows ドライバーの今後の要件のプレビューを提供します。  

> [!NOTE]
> Windows ドライバーと Windows デスクトップ ドライバーの違いは、Windows 10 バージョン 2004 で提出、認定されているドライバーに影響を及ぼしません。  認定と提出に関する変更は後日行われます。


## <a name="windows-drivers-requirements"></a>Windows ドライバーの要件

Windows ドライバーが認定オプションになる場合、次の要件が適用されます。

- [DCH 設計原則](dch-principles-best-practices.md)に準拠している。
- [ドライバー パッケージの分離](driver-isolation.md)の原則に従っている。
- [API レイヤー化の要件](api-layering.md)に従っている。
- [ハードウェア ラボ キット](https://docs.microsoft.com/windows-hardware/test/hlk/)を使用して、[Windows ハードウェア互換性プログラムの認定プロセス](https://docs.microsoft.com/windows-hardware/design/compatibility/whcp-certification-process)で認定されている。 Windows ハードウェア互換性プログラムの認定プロセスの要件は、KMDF と UMDF の両方のドライバーに適用されることに注意してください。

## <a name="windows-drivers-vs-windows-desktop-drivers"></a>Windows ドライバーとWindows デスクトップ ドライバー

次の表は、上記の違いをまとめたものです。

|                                                                     |Windows ドライバー|Windows デスクトップ ドライバー |
| --------------------------------------------------------------------|:-------------:|:----------------------:|
| Windows 10 デスクトップで実行                                           | はい           | はい                    |
| Windows 10X で実行                                                  | はい           | いいえ                     |
| WHCP の認定が必要                                         | はい           | いいえ                     |
| WDK および HLK がドライバーの開発と認定を行うための主な手段| はい           | はい                    |
| 信頼性とサービス性の要件     | はい           | いいえ                     |


Windows 10 デスクトップのみで実行されるドライバーは Windows ドライバーの追加の要件を満たす必要がありませんが、そうすることで、ドライバーのサービス性と信頼性を高め、将来の Windows 10X での認定に備えることができます。
