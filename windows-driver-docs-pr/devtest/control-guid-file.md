---
title: コントロール GUID ファイル
description: コントロール GUID ファイル
ms.assetid: cf5dd9bf-c9db-4324-abd3-ee0e1b15e14d
keywords:
- コントロール Guid WDK
- .ctl ファイル
- ctl ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a3288402a4bb5d59047fa389c521fae3acb6bcd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343082"
---
# <a name="control-guid-file"></a>コントロール GUID ファイル

## <span id="ddk_control_guid_file_tools"></span><span id="DDK_CONTROL_GUID_FILE_TOOLS"></span>

*制御 GUID ファイル*(.ctl 拡張子) は、テキスト ファイルを指定する、[コントロール GUID](control-guid.md)トレース プロバイダーの形式の GUID のフレンドリ名。

```
ControlGUID GUIDFriendlyName
```

トレース プロバイダーの開発者は、通常、このファイルを指定します。 トレース プロバイダーのソース コードがあれば、GUID と GUID のフレンドリ名を検索し、制御 GUID ファイルを作成できます。

ソース コードでの定義を見つけ、 [WPP\_コントロール\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff556186)マクロ。 GUID 値と GUID のフレンドリ名が表示されます次の例では太字です。

```C
#define WPP_CONTROL_GUIDS \
    WPP_DEFINE_CONTROL_GUID(GUIDFriendlyName, (ControlGUID),  \
        WPP_DEFINE_BIT(NameOfTraceFlag1)  \
        WPP_DEFINE_BIT(NameOfTraceFlag2)  \
        .............................   \
        .............................   \
        WPP_DEFINE_BIT(NameOfTraceFlag31) )
```
