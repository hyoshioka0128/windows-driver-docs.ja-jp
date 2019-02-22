---
title: 書き込みコア ドライバー
description: 書き込みコア ドライバー
ms.assetid: 3a41a91b-3cc3-462a-8836-448203ccb4c2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f3a540cb9c657a470872dd52be14c5b36b8b646
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557895"
---
# <a name="writing-core-drivers"></a>書き込みコア ドライバー


ライターの印刷ドライバーでは、Windows Vista では、中核となるドライバーの機能を使用できます。 コア ドライバーを作成するには、コア ドライバーを構成する一連のファイルを参照するその他のドライバー パッケージが使用できる GUID を生成します。 たとえば、Ntprint.inf では、次の例では Unidrv core ドライバー ファイルの定義が表示します。

```cpp
[Microsoft.NTx86]
"{D20EA372-DD35-4950-9ED8-A6335AFE79F0}" =  
  {D20EA372-DD35-4950-9ED8-A6335AFE79F0}, 
  {D20EA372-DD35-4950-9ED8-A6335AFE79F0}
[{D20EA372-DD35-4950-9ED8-A6335AFE79F0}]
CopyFiles=UNIDRV,PJLMON.DLL,@TTFSUB.GPD,@LOCALE.GPD,@MSXPSINC.GPD
[UNIDRV]
; Unidrv files and pjlmon sections follow...
```

この定義での印刷ドライバーの INF ファイルをファイルを参照できます core ドライバーを使用して、 **CoreDriverSections**キーワードの前の例で示すようにします。

コア ドライバーが以前のバージョンとの互換性を保持する必要がありますに注意してください。 1 つ以上のドライバーは、コア ドライバーを使用してためは、既存のドライバーが更新されると、それに依存する操作を続行する必要があります。 コア ドライバーをドライバー パッケージの一部として出荷する必要があります。

コア ドライバーは、コア ドライバー GUID であるデバイスの説明が含まれています、モデルのセクションで定義されます。 次に、例を示します。

```cpp
; Model section
[Company.NTx86]
"{GUID1}" = {GUID1}, {GUID1}

; Install section - must list all files in the core printer driver
[{GUID1}]
DriverVer = MM/DD/YYYY,1.1.1.1
CopyFiles=MANUFACTURER_CORE_FILESET

; Core Driver Section, can use print-specific INF keywords here
[MANUFACTURER_CORE]
CopyFiles=MANUFACTURER_CORE_FILESET

[MANUFACTURER_CORE_FILESET]
File1.dll
File2.dll
File3.dll

[ControlFlags]
AlwaysExcludeFromSelect = {GUID1}
```

コア ドライバーを使用して、インストール」にバージョン情報を含める必要があります、 **DriverVer**キーワード。 インストールのセクションでは、コア ドライバーを必要とするすべてのファイルも表示する必要があります。 使用して、新しい**AlwaysExcludeFromSelect**キーワードをコア ドライバーが、ユーザーが UI に表示されないことを確認します。

 

 




