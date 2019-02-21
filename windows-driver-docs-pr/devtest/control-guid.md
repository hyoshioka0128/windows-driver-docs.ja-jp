---
title: コントロールの GUID
description: コントロールの GUID
ms.assetid: a85a5e1a-c4c1-40d4-a0ef-d8e552590f03
keywords:
- コントロール Guid WDK
- Guid の WDK ソフトウェア トレース
- 識別子の WDK ソフトウェア トレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 191806f223c1d44d3aeb54f48f297adf5cc600b6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538280"
---
# <a name="control-guid"></a>コントロールの GUID

## <span id="ddk_control_guid_tools"></span><span id="DDK_CONTROL_GUID_TOOLS"></span>

各[トレース プロバイダー](trace-provider.md)定義、*コントロール GUID*プロバイダーを一意に識別します。 この GUID の使用を有効または、使用して、トレース プロバイダーを無効にする[Event Tracing for Windows (ETW)](event-tracing-for-windows--etw-.md)します。

GUID は、コントロール、 [WPP\_コントロール\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff556186)をインストルメント化されたトレース プロバイダーのソース コード ファイルでマクロ。

```C
#define WPP_CONTROL_GUIDS \
    WPP_DEFINE_CONTROL_GUID(GUIDFriendlyName, (ControlGUID),  \
        WPP_DEFINE_BIT(NameOfTraceFlag1)  \
        WPP_DEFINE_BIT(NameOfTraceFlag2)  \
        .............................   \
        .............................   \
        WPP_DEFINE_BIT(NameOfTraceFlag31) )
```

[Tracepdb](tracepdb.md)作成、[トレース (MOF) ファイル](trace-managed-object-format--mof--file.md)コントロールの GUID と PDB ファイルで表される各トレース プロバイダーのトレース レベルを格納しています。 MOF ファイルの名前は、トレース プロバイダーのモジュールの名前です。 Tracepdb も生成できる TMC ファイルを使用する場合、 **-c**オプション。

定義のスコープを再定義し、コントロールの GUID を使用するには、コントロールの GUID は、etw トレース プロバイダーが識別されるため、[トレース プロバイダー](trace-provider.md)します。 たとえば、複数のドライバーは同じコントロールの GUID を指定することで 1 つのトレース プロバイダーの一部をすることができます。 または、1 つのドライバーの各インスタンスで別のコントロールの Guid を指定することによって複数のトレース プロバイダーを含めることができます、 [WPP\_コントロール\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff556186)マクロ。
