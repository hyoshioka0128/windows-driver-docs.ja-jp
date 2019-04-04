---
title: wdfkd.wdflogsave
description: Wdfkd.wdflogsave 拡張機能は、カーネル モード ドライバー フレームワーク (KMDF) エラー、指定したドライバーのログ レコードを traceview でを使用して表示できるイベントのトレース ログ (.etl) ファイルに保存します。
ms.assetid: e072d522-a418-4afb-8434-c6355d026770
keywords:
- デバッグ wdfkd.wdflogsave Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdflogsave
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: edf5e0724182de80f2fdd85f2f0727ae97eb1f47
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558969"
---
# <a name="wdfkdwdflogsave"></a>!wdfkd.wdflogsave


**! Wdfkd.wdflogsave**拡張機能は traceview でを使用して表示できるイベントのトレース ログ (.etl) ファイルに、カーネル モード ドライバー フレームワーク (KMDF) エラーに、指定したドライバーのログ レコードを保存します。

```dbgcmd
!wdfkd.wdflogsave [DriverName [FileName]]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______DriverName______"></span><span id="_______drivername______"></span><span id="_______DRIVERNAME______"></span> *ドライバー名*   
(省略可能)。 ドライバーの名前。 *DriverName* .sys ファイル名拡張子を含めることはできません。

<span id="_______FileName______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span> *FileName*   
(省略可能)。 KMDF エラーのログ レコードの保存先ファイルの名前。 *ファイル名*.etl ファイル名拡張子を含めないでください。 省略した場合*FileName*、KMDF エラー ログの記録が DriverName.etl ファイルに保存されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Wdfkd.dll

### <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク

KMDF 1、UMDF 2

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)を参照してください。

<a name="remarks"></a>注釈
-------

省略した場合、 *DriverName*パラメーター、既定のドライバー名を使用します。 使用して、 [ **! wdfkd.wdfgetdriver** ](-wdfkd-wdfgetdriver.md)既定ドライバーの名前を表示して使用する拡張機能、 [ **! wdfkd.wdfsetdriver** ](-wdfkd-wdfsetdriver.md)の拡張機能既定のドライバーの名前を設定します。

 

 





