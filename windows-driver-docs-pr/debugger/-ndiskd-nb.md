---
title: ndiskd.nb
description: Ndiskd.nb 拡張機能では、NET_BUFFER (NB) 構造に関する情報が表示されます。
ms.assetid: 7351264c-4adc-43ac-9eca-41deb3d35983
keywords:
- デバッグ ndiskd.nb Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.nb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 551b052fd37431742bcbe75d9789c3f8b5fb9b92
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363136"
---
# <a name="ndiskdnb"></a>!ndiskd.nb


**! Ndiskd.nb**拡張機能に関する情報を表示する、 [ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-structure) (NB) 構造体。

```console
!ndiskd.nb [-handle <x>] [-verbosity <x>] [-basic] [-chain] [-data] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必須。 アドレスを**NET\_バッファー**構造体。

<span id="_______-verbosity______"></span><span id="_______-VERBOSITY______"></span> *-verbosity*   
表示する詳細のレベルです。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span> *-basic*   
NB. に関する基本情報を表示します。

<span id="_______-chain______"></span><span id="_______-CHAIN______"></span> *チェーン*   
関連付けられた、NB. MDLs をすべてを表示します。

<span id="_______-data______"></span><span id="_______-DATA______"></span> *-data*   
NB. の実際のデータ ペイロードをダンプします。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>例
--------

**NET\_バッファー**から取得された次の例では、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)の例」の「[ **! ndiskd.nbl** ](-ndiskd-nbl.md)トピック。 NB のハンドルは、ffffdf8014952610 です。

```console
2: kd> !ndiskd.nbl ffffdf80149524a0 -data
NET_BUFFER ffffdf8014952610
```

クリックすることができます、 **NET\_バッファー**のハンドルまたはを実行、 **! ndiskd.nb-処理**コマンドをその詳細を参照してください。

```console
2: kd> !ndiskd.nb ffffdf8014952610
    NB                 ffffdf8014952610    Next NB            0
    Length             0                   Source pool        ffffdf80147e4a40
    First MDL          ffffdf8014a37930    DataOffset         0
    Current MDL        [First MDL]         Current MDL offset 0

    View associated NBL
```

使用して、 **! ndiskd.nb-チェーン**これを確認するコマンド**NET\_バッファー**のだけでなく、基本的な詳細 MDL チェーン。 次の例では、1 つだけ MDL があります。 そのハンドルは、ffffdf8014a37930 です。

```console
2: kd> !ndiskd.nb ffffdf8014952610 -chain
    NB                 ffffdf8014952610    Next NB            0
    Length             0                   Source pool        ffffdf80147e4a40
    First MDL          ffffdf8014a37930    DataOffset         0
    Current MDL        [First MDL]         Current MDL offset 0
        MDL [current]      ffffdf8014a37930    MDL Flags             c
        MappedSystemVa     ffffdf8014bf0024    ByteCount          0n1514
        Process            [System process]    ByteOffset         0n36  
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-structure)

[**NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)

[ **!ndiskd.nbl**](-ndiskd-nbl.md)

 

 






