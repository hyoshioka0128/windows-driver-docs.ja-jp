---
title: ndiskd ミニドライバー
description: ミニドライバーコマンドは、NDIS ミニポートドライバーに関する情報を表示します。
ms.assetid: CD349B10-8363-4D48-A830-CC9EF5EA75BF
keywords:
- ミニドライバー Windows デバッグ
ms.date: 06/15/2020
topic_type:
- apiref
api_name:
- ndiskd.minidriver
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ad2fc33e2c763bdff36450f3d59f9f4fc19bef8c
ms.sourcegitcommit: 8596782b07c8a71adf38fc2c2da68b75ba0a1259
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85593940"
---
# <a name="ndiskdminidriver"></a>!ndiskd.minidriver

**ミニドライバー**コマンドは、NDIS ミニポートドライバーに関する情報を表示します。 パラメーターを使用せずにこの拡張機能を実行すると、システムでアクティブになっている NDIS ミニポートドライバーの一覧がによって表示されます。

```console
!ndiskd.minidriver [-handle <x>] [-basic] [-miniports] [-devices] [-handlers]
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>パラメータ

<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-ハンドル*   
NDIS ミニポートドライバーの省略可能なハンドル。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span>*-基本*   
ミニポートドライバーに関する基本的な情報を表示します。

<span id="_______-miniports______"></span><span id="_______-MINIPORTS______"></span>*-ミニポート*   
このミニポートドライバーに関連付けられているミニポートを表示します。

<span id="_______-devices______"></span><span id="_______-DEVICES______"></span>*-デバイス*   
このミニポートドライバーに関連付けられているデバイスを表示します。

<span id="_______-handlers______"></span><span id="_______-HANDLERS______"></span>*-ハンドラー*   
このドライバーのミニポートハンドラーを表示します。

## <a name="dll"></a>[DLL]

Ndiskd.dll

## <a name="examples"></a>例

システムでアクティブになっているすべての NDIS ミニポートドライバーの一覧を取得するには、パラメーターを指定せずに **! ndiskd ミニドライバー**コマンドを入力します。 次の例では、kdnic アダプターのハンドル、ffffd20d12dec020 を探します。

```console
1: kd> !ndiskd.minidriver -basic
    ffffd20d173deae0 - tunnel
    ffffd20d12dec020 - kdnic
```

Kdnic アダプターのハンドルを使用して、ハンドルをクリックするか、 **! ndiskd ミニドライバー**コマンドを入力して、トンネルミニポートドライバーの詳細情報と、関連付けられているミニポートの一覧を確認できるようになりました。

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

## <a name="see-also"></a>関連項目

[ネットワーク ドライバー設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)
