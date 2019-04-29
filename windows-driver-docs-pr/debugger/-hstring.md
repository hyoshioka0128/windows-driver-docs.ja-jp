---
title: hstring
description: Hstring 拡張機能には、HSTRING のフィールドが表示されます。 表示の最後の項目は、文字列自体です。
ms.assetid: 6FB85609-0FB1-457E-A58E-804F69016406
keywords:
- Windows デバッグ hstring
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- hstring
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8c41b63cde736165acf39cf9554be488c0bffbb6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336459"
---
# <a name="hstring"></a>!hstring


**! Hstring**のフィールドに表示拡張機能、 **HSTRING**します。 表示の最後の項目は、文字列自体です。

```dbgcmd
!hstring Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="Address"></span><span id="address"></span><span id="ADDRESS"></span>*アドレス*  
アドレス、 **HSTRING**します。

<a name="remarks"></a>注釈
-------

**HSTRING**データ型は、NULL 文字が埋め込まれている文字列をサポートしています。 ただし、 **! hstring**拡張機能には、最初の NULL 文字までしか文字列が表示されます。 埋め込まれた NULL 文字を含む文字列全体を表示するには、使用、 [ **! hstring2** ](-hstring2.md)拡張機能。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[Windows ランタイムのデバッガー コマンド](windows-runtime-debugger-commands.md)

[**!hstring2**](-hstring2.md)

[**!winrterr**](-winrterr.md)

 

 






