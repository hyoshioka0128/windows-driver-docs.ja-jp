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
ms.openlocfilehash: db5c212feb92780f3a19423fc0c53067965d8c58
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371590"
---
# <a name="control-guid-file"></a>コントロール GUID ファイル

## <span id="ddk_control_guid_file_tools"></span><span id="DDK_CONTROL_GUID_FILE_TOOLS"></span>

*制御 GUID ファイル*(.ctl 拡張子) は、テキスト ファイルを指定する、[コントロール GUID](control-guid.md)トレース プロバイダーの形式の GUID のフレンドリ名。

```
ControlGUID GUIDFriendlyName
```

トレース プロバイダーの開発者は、通常、このファイルを指定します。 トレース プロバイダーのソース コードがあれば、GUID と GUID のフレンドリ名を検索し、制御 GUID ファイルを作成できます。

ソース コードでの定義を見つけ、 [WPP\_コントロール\_GUID](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))マクロ。 GUID 値と GUID のフレンドリ名が表示されます次の例では太字です。

```C
#define WPP_CONTROL_GUIDS \
    WPP_DEFINE_CONTROL_GUID(GUIDFriendlyName, (ControlGUID),  \
        WPP_DEFINE_BIT(NameOfTraceFlag1)  \
        WPP_DEFINE_BIT(NameOfTraceFlag2)  \
        .............................   \
        .............................   \
        WPP_DEFINE_BIT(NameOfTraceFlag31) )
```
