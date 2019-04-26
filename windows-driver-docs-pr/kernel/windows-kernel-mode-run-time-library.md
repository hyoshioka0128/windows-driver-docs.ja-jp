---
title: Windows カーネルモード ランタイム ライブラリ
description: Windows カーネルモード ランタイム ライブラリ
ms.assetid: 9c968014-c529-43e1-a8a6-a307c90e4162
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 45dc66eb907a2c50f063a22a7beef4dd368c9aca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357532"
---
# <a name="windows-kernel-mode-run-time-library"></a>Windows カーネルモード ランタイム ライブラリ


Windows では、さまざまなカーネル モード コンポーネントに必要な共通のユーティリティ ルーチンのセットを提供します。 たとえば、 [ **RtlCheckRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff561754)指定されたキーがレジストリにするために使用します。

ランタイム ライブラリ (RTL) ルーチンのほとんどの文字が付いて"**Rtl**"は、カーネルのランタイム ライブラリ ルーチンの一覧を参照してください。[ランタイム ライブラリ (RTL) のルーチン](https://msdn.microsoft.com/library/windows/hardware/ff563638)します。

安全な文字列処理用にデザインされたカーネル モードのさまざまなライブラリもあります。 文字列の安全なライブラリの詳細については、次を参照してください。 [Windows カーネル モードの安全な文字列ライブラリ](windows-kernel-mode-safe-string-library.md)します。 ライブラリ ルーチンの安全な文字列にはプレフィックスも通常ことに注意してください。"**Rtl**"が、ランタイム ライブラリ (RTL) の一部ではありません。

 

 




