---
title: TxtSetup.oem ファイルの既定値のセクション
description: 既定値のセクションでは、このファイルでサポートされる各ハードウェア コンポーネントの既定のドライバーが一覧表示します。 Windows では、ユーザーにドライバーの一覧を表示するときに、既定の選択が強調表示されます。
ms.assetid: 5f7fc7c8-543d-442a-911d-320aa19c72f0
keywords:
- 既定値のセクションの TxtSetup.oem ファイルのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- Defaults Section of a TxtSetup.oem File
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7c98d6f4028da4a476219e87393a656d8e1e9603
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553216"
---
# <a name="defaults-section-of-a-txtsetupoem-file"></a>TxtSetup.oem ファイルの既定値のセクション


**既定**セクションには、このファイルでサポートされる各ハードウェア コンポーネントの既定のドライバーが一覧表示されます。 Windows では、ユーザーにドライバーの一覧を表示するときに、既定の選択が強調表示されます。

``` syntax
[Defaults]
component = ID
...
```

<a href="" id="component"></a>*コンポーネント*  
このファイルでサポートされるハードウェア コンポーネントを指定します。 *コンポーネント*次のシステム定義の値のいずれかを指定する必要があります:**コンピューター**または**scsi**します。

<a href="" id="id"></a>*ID*  
既定のオプションを識別する文字列を指定します。 この文字列には、対応する指定された ID が一致する*HwComponent*セクション。

場合、 *TxtSetup.oem*ファイルがサポートされているコンポーネントの既定のドライバーを定義する失敗した場合、Windows の最初のエントリを使用して、 *HwComponent*セクション。

次の例は、**の既定値**セクション (および*HwComponent*セクション) の*TxtSetup.oem* 1 つのコンポーネントをサポートするファイル (**scsi**):

``` syntax
; ...
[Defaults]
SCSI = oemscsi
 
[SCSI]                  ; HwComponent section
oemscsi = "OEM Fast SCSI Controller"
oemscsi2 = "OEM Fast SCSI Controller 2"
 
; ...
```

 

 





