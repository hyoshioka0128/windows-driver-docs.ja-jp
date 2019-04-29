---
title: wdfkd.wdfsetdriver
description: Wdfkd.wdfsetdriver 拡張機能は、拡張機能のデバッガー コマンドを適用する既定のカーネル モード ドライバー フレームワーク (KMDF) ドライバーの名前を設定します。
ms.assetid: 90fc99a0-1e78-44bb-ba91-191f116160e7
keywords:
- デバッグ wdfkd.wdfsetdriver Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfsetdriver
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1e7e5457c64ab31256a4b5b2a9dc4947b5f41b9c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323269"
---
# <a name="wdfkdwdfsetdriver"></a>!wdfkd.wdfsetdriver


**! Wdfkd.wdfsetdriver**拡張機能が拡張機能のコマンドを適用するデバッガーを既定のカーネル モード ドライバー フレームワーク (KMDF) ドライバーの名前を設定します。

```dbgcmd
!wdfkd.wdfsetdriver DriverName
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span> *ドライバー名*   
ドライバーの名前。 *DriverName* .sys ファイル名拡張子を含めることはできません。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF 1、UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)します。

<a name="remarks"></a>注釈
-------

**! Wdfkd.wdfsetdriver**拡張機能は、既定のドライバーの名前を設定します。 この名前を使用するには他の**wdfkd**ドライバー名を指定することは拡張機能。

現在の既定 KMDF ドライバーの名前を取得する、 [ **! wdfkd.wdfgetdriver** ](-wdfkd-wdfgetdriver.md)拡張機能。

 

 





