---
title: Windows カーネルモード ランタイム ライブラリ
description: Windows カーネルモード ランタイム ライブラリ
ms.assetid: 9c968014-c529-43e1-a8a6-a307c90e4162
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 139c31f28a86cae28bfe894f3a04b3a520cfa0cf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838307"
---
# <a name="windows-kernel-mode-run-time-library"></a>Windows カーネルモード ランタイム ライブラリ


Windows には、さまざまなカーネルモードコンポーネントで必要となる一般的なユーティリティルーチンのセットが用意されています。 たとえば、特定のキーがレジストリ内に存在するかどうかを確認するには、 [**Rtlcheckregistrykey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlcheckregistrykey)を使用します。

ほとんどのランタイムライブラリ (RTL) ルーチンには、先頭に "**rtl**" という文字が付いています。カーネルのランタイムライブラリルーチンの一覧については、「[ランタイムライブラリ (RTL) ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

また、安全な文字列処理用に特別に設計された別のカーネルモードライブラリもあります。 安全な文字列ライブラリの詳細については、「 [Windows カーネルモードのセーフ文字列ライブラリ](windows-kernel-mode-safe-string-library.md)」を参照してください。 安全な文字列ライブラリルーチンも、通常は "**rtl**" というプレフィックスが付いていますが、ランタイムライブラリ (rtl) の一部ではないことに注意してください。

 

 




