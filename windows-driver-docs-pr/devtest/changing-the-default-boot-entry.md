---
title: 既定のブート エントリの変更
description: 既定のブート エントリの変更
ms.assetid: 0dce10d4-f73a-49bd-8a24-a4aa14c82233
keywords:
- 既定のブート エントリ
- Boot.ini ファイル WDK、既定のブート エントリ
- ブート オプション WDK、既定のブート エントリ
- ブート エントリを識別します。
- WDK の現在のブート エントリ
- NVRAM ブート オプション WDK、既定のブート エントリ
- EFI NVRAM ブート オプション WDK、既定のブート エントリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a5f6f5e29e977095c2b28f19feb08199c11a37a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344054"
---
# <a name="changing-the-default-boot-entry"></a>既定のブート エントリの変更


## <span id="ddk_changing_the_default_boot_entry_tools"></span><span id="DDK_CHANGING_THE_DEFAULT_BOOT_ENTRY_TOOLS"></span>


既定のブート エントリが、ブート メニュー タイムアウトを過ぎると、ブート ローダーを選択します。 必要なオペレーティング システムの構成が自動的に読み込まれていることを確認する既定のブート エントリを変更することができます。

Windows、既定のブート エントリを変更するのに BCDEdit を使用することができます。

### <a name="span-idusingbcdeditspanspan-idusingbcdeditspanusing-bcdedit"></a><span id="using_bcdedit"></span><span id="USING_BCDEDIT"></span>BCDEdit を使用してください。

使用して既定ブート エントリを指定できます、 **既定/** オプション。 既定のオペレーティング システムを指定する構文は次のとおりです。

```
bcdedit /default <ID>
```

*&lt;ID&gt;* は既定値として指定するオペレーティング システムに関連付けられている Windows ブート ローダーのブート エントリの GUID です。 中かっこを含める必要があります ( **{}** ) 例については、guid:

```
bcdedit /default {cbd971bf-b7b8-4885-951a-fa03044f5d71}
```

マルチブート コンピューターでは、以前の Windows オペレーティング システム ローダーには、既定のブート エントリを変更するには、設定 *&lt;ID&gt;* に **{ntldr}** GUID の予約名であります。Ntldr と関連付けられています。 これは、Boot.ini ファイル内のエントリによって別のメニューが表示します。

```
bcdedit /default {ntldr}
```

 

 





