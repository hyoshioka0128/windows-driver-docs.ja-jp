---
title: wdfkd_wdfumtriage
description: Wdfkd_wdfumtriage 拡張機能には、デバイス オブジェクト、読み込まれているドライバーの PnP デバイス スタック、クラスの拡張機能など、システム上のデバイスの UMDF Irp のディスパッチ情報が表示されます。
ms.assetid: E25DAE56-E42A-4A56-B36F-8B0B1D826524
keywords:
- Windows デバッグ wdfkd_wdfumtriage
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wdfkd_wdfumtriage
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 36146a80a288aabc380f7d9afa757fa0f335d191
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539743"
---
# <a name="wdfkdwdfumtriage"></a>! wdfkd\_wdfumtriage


**! Wdfkd\_wdfumtriage**拡張機能は、対応するホスト プロセス、読み込まれているドライバーとクラスの拡張機能、PnP デバイス スタック、PnP デバイスのデバイス オブジェクトを含む、システムで UMDF のすべてのデバイスに関する情報を表示しますIrp、および問題の状態が該当する場合、ノードがディスパッチされます。

```dbgcmd
!wdfkd.wdfumtriage
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Wdfkd.dll

## <a name="span-idframeworksspanspan-idframeworksspanspan-idframeworksspanframeworks"></a><span id="Frameworks"></span><span id="frameworks"></span><span id="FRAMEWORKS"></span>フレームワーク


UMDF 2

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報


詳細については、次を参照してください。[カーネル モード ドライバー フレームワークのデバッグ](kernel-mode-driver-framework-debugging.md)します。

<a name="remarks"></a>注釈
-------

このコマンドは、カーネル モードのデバッグ セッションで使用できます。

出力の例を次に示します **! wdfkd\_wdfumtriage**します。

![ドライバーのオブジェクト一覧の出力から! wdfkd.wdfumtriage](images/wdfumtriage2.png)

 

 





