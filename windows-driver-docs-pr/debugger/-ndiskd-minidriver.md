---
title: ndiskd.minidriver
description: Ndiskd.minidriver コマンドでは、NDIS ミニポート ドライバーに関する情報が表示されます。
ms.assetid: CD349B10-8363-4D48-A830-CC9EF5EA75BF
keywords:
- デバッグ ndiskd.minidriver Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.minidriver
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 725517285a9e0ad45933f3b8a070d49f5f561fda
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365760"
---
# <a name="ndiskdminidriver"></a>!ndiskd.minidriver


**! Ndiskd.minidriver**コマンドは、NDIS ミニポート ドライバーに関する情報を表示します。 パラメーターなしで、この拡張機能を実行する場合。 ndiskd システムでアクティブな NDIS ミニポート ドライバーの一覧が表示されます。

```console
!ndiskd.minidriver [-handle <x>] [-basic] [-miniports] [-devices] [-handlers] 
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
NDIS ミニポート ドライバーのハンドル。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span> *-basic*   
ミニポート ドライバーに関する基本情報が表示されます。

<span id="_______-miniports______"></span><span id="_______-MINIPORTS______"></span> *-ミニポート*   
このミニポート ドライバーに関連付けられているミニポートが表示されます。

<span id="_______-devices______"></span><span id="_______-DEVICES______"></span> *-デバイス*   
このミニポート ドライバーに関連付けられているデバイスが表示されます。

<span id="_______-handlers______"></span><span id="_______-HANDLERS______"></span> *-ハンドラー*   
このドライバーのミニポート ハンドラーが表示されます。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Ndiskd.dll

<a name="examples"></a>例
--------

入力、 **! ndiskd.minidriver**コマンドとパラメーターのないシステムでアクティブなすべての NDIS ミニポート ドライバーの一覧を取得します。 次の例では、検索、kdnic アダプターのハンドル、ffffd20d12dec020

```console
1: kd> !ndiskd.minidriver -basic
    ffffd20d173deae0 - tunnel
    ffffd20d12dec020 - kdnic
```

Kdnic アダプターのハンドルを使用して、できるようになりましたハンドルをクリックしてまたは入力した、 **! ndiskd.minidriver-処理**コマンドに関連付けられているミニポートの一覧と同様に、トンネルのミニポート ドライバーの詳細情報を参照してください。

```console
1: kd> !ndiskd.minidriver ffffd20d12dec020


MINIPORT DRIVER

    kdnic

    Ndis handle        ffffd20d12dec020    [type it]
    Driver context     fffff80d2fa15100
    DRIVER_OBJECT      ffffd20d12dee540
    Driver image       kdnic.sys
    Registry path      \REGISTRY\MACHINE\SYSTEM\ControlSet001\Services\kdnic
    Reference Count    2
    Flags              [No flags set]


MINIPORTS

    Miniport                                                                    
    ffffd20d12dd71a0 - Microsoft Kernel Debug Network Adapter

    Handlers
    Device objects
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

 

 






