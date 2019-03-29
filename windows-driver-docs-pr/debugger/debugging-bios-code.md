---
title: BIOS コードのデバッグ
description: BIOS コードのデバッグ
ms.assetid: 98f0381b-4f9d-4cf2-9860-8da20f6fbd38
keywords:
- BIOS のデバッグ
- BIOS のデバッグの概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2fe03c8240da0461ae35cc0be39f02750f110dd5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577798"
---
# <a name="debugging-bios-code"></a>BIOS コードのデバッグ


## <span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>


さまざまなデバッグ技術が必要ですので、BIOS のコードは、標準のアセンブリのコードから組み込まれていません。

X86 ベースのプロセッサでは、BIOS は、16 ビットのコードを使用します。 このコードを逆アセンブルするには、使用、 [ **ux (Unassemble x86 BIOS)** ](ux--unassemble-x86-bios-.md)コマンド。 Intel マルチプロセッサ仕様 (MP) についての情報を表示するには、使用、 [ **! mp** ](-mps.md)拡張機能。

ACPI BIOS コードをデバッグする場合、上記のコマンドは機能しません、ACPI BIOS は ACPI 機械語 (AML) に書き込まれるため。 このコードを逆アセンブルを使用する必要があります[ **! amli u**](-amli-u.md)します。 この種のデバッグの詳細については、次を参照してください。 [ACPI デバッグ](acpi-debugging.md)します。

 

 





