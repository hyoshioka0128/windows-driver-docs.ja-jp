---
title: wdfkd.wdfumtriage
description: Wdfkd.wdfumtriage 拡張機能には、デバイス オブジェクト、読み込まれているドライバーの PnP デバイス スタック、クラスの拡張機能など、システム上のデバイスの UMDF Irp のディスパッチ情報が表示されます。
ms.assetid: E25DAE56-E42A-4A56-B36F-8B0B1D826524
keywords:
- デバッグ wdfkd.wdfumtriage Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd.wdfumtriage
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1d26b1e3681eae2dcc9fb43bef66d25da03c0e13
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902566"
---
# <a name="wdfkdwdfumtriage"></a>!wdfkd.wdfumtriage


**! Wdfkd.wdfumtriage**拡張機能は、システム、デバイス オブジェクトを含む、対応するホスト プロセス、読み込まれているドライバーとクラスの拡張機能、PnP デバイス スタック、PnP デバイス ノードの場合は、UMDF のすべてのデバイスに関する情報を表示しますIrp、および該当する場合、問題の状態をディスパッチします。

```dbgcmd
!wdfkd.wdfumtriage
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Wdfkd.dll

## <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク


UMDF 2

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報


詳細については、次を参照してください。[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)します。

<a name="remarks"></a>コメント
-------

このコマンドは、カーネル モードのデバッグ セッションで使用できます。

出力の例を次に示します **! wdfkd.wdfumtriage**します。

![ドライバーのオブジェクト一覧の出力から! wdfkd.wdfumtriage](images/wdfumtriage2.png)

 

 





