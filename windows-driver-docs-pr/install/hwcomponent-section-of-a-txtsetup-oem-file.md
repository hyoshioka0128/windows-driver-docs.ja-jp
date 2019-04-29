---
title: TxtSetup.oem ファイルの HwComponent セクション
description: HwComponent セクションには、特定のコンポーネントの使用可能なドライバーが一覧表示します。 ファイルでサポートされているコンポーネントの種類ごとに HwComponent セクションがあります。
ms.assetid: 84ba057b-6699-4709-bee8-24cb555d4165
keywords:
- HwComponent セクションの TxtSetup.oem ファイルのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- HwComponent Section of a TxtSetup.oem File
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3f21243aee18b677491771bb518464148b2d7db4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386917"
---
# <a name="hwcomponent-section-of-a-txtsetupoem-file"></a>TxtSetup.oem ファイルの HwComponent セクション


A *HwComponent*セクションには、特定のコンポーネントの使用可能なドライバーが一覧表示されます。 *HwComponent*ファイルでサポートされているコンポーネントの種類ごとにセクション。

``` syntax
[HwComponent]
ID = description
...
```

<a href="" id="hwcomponent"></a>*HwComponent*  
セクションの名前は、次のシステム定義の値のいずれかを指定する必要があります:**コンピューター**または**scsi**します。

<a href="" id="id"></a>*ID*  
ここでは、オプションを識別する内で一意で、文字列を指定します。

このセクションでは、各エントリの必要があります、対応する**ファイル**。<em>HwComponent</em>**.**<em>ID</em>ファイルのセクション。

**コンピューター**コンポーネント、カーネルの Windows のコピー、文字列の最後の 3 つの文字を決定します。 この文字列は、「(_u)」で終了した場合、Windows はユニプロセッサ カーネルをコピーします。 この文字列は、"_mp"で終了した場合、Windows は、マルチプロセッサのカーネルをコピーします。 文字列が"_Xp"で終わっていない場合 Windows いずれか、またはその他のカーネルをコピーしますがどれでは保証されません。

<a href="" id="description"></a>*説明*  
Windows はドライバーの選択肢のメニューで、ユーザーに提示する文字列を指定します。

次の例は、 *HwComponent*のセクションを*TxtSetup.oem* 1 つのコンポーネントをサポートするファイル (**scsi**) し、2 つのオプションを提供します。

``` syntax
; ...
[SCSI]                  ; HwComponent section
oemscsi = "OEM Fast SCSI Controller"
oemscsi2 = "OEM Fast SCSI Controller 2"
 
; ...
```

 

 





