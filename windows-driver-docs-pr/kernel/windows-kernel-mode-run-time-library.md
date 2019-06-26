---
title: Windows カーネルモード ランタイム ライブラリ
description: Windows カーネルモード ランタイム ライブラリ
ms.assetid: 9c968014-c529-43e1-a8a6-a307c90e4162
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1adf71f4f0eab0d05c9b809bb411f35ad2c65fbe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374168"
---
# <a name="windows-kernel-mode-run-time-library"></a>Windows カーネルモード ランタイム ライブラリ


Windows では、さまざまなカーネル モード コンポーネントに必要な共通のユーティリティ ルーチンのセットを提供します。 たとえば、 [ **RtlCheckRegistryKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlcheckregistrykey)指定されたキーがレジストリにするために使用します。

ランタイム ライブラリ (RTL) ルーチンのほとんどの文字が付いて"**Rtl**"は、カーネルのランタイム ライブラリ ルーチンの一覧を参照してください。[ランタイム ライブラリ (RTL) のルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

安全な文字列処理用にデザインされたカーネル モードのさまざまなライブラリもあります。 文字列の安全なライブラリの詳細については、次を参照してください。 [Windows カーネル モードの安全な文字列ライブラリ](windows-kernel-mode-safe-string-library.md)します。 ライブラリ ルーチンの安全な文字列にはプレフィックスも通常ことに注意してください。"**Rtl**"が、ランタイム ライブラリ (RTL) の一部ではありません。

 

 




