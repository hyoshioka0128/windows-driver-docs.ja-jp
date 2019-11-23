---
title: ndiskd nb
description: Ndiskd nb 拡張子は、NET_BUFFER (NB) 構造に関する情報を表示します。
ms.assetid: 7351264c-4adc-43ac-9eca-41deb3d35983
keywords:
- ndiskd nb Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.nb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7fb01044dde6b95e312f1de17561d5ac9515c3b6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826650"
---
# <a name="ndiskdnb"></a>!ndiskd.nb


**! Ndiskd nb**拡張機能には、 [**NET\_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-structure) (nb) 構造に関する情報が表示されます。

```console
!ndiskd.nb [-handle <x>] [-verbosity <x>] [-basic] [-chain] [-data] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-  を処理*します  
必須。 **NET\_のバッファー**構造のアドレス。

<span id="_______-verbosity______"></span><span id="_______-VERBOSITY______"></span> *-詳細*   
表示する詳細レベル。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span> *-基本*   
NB に関する基本的な情報を表示します。

<span id="_______-chain______"></span><span id="_______-CHAIN______"></span> *-チェーン*   
NB に関連付けられているすべての MDLs を表示します。

<span id="_______-data______"></span><span id="_______-DATA______"></span> *-データ*   
NB の実際のデータペイロードをダンプします。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

<a name="examples"></a>例
--------

次の例の**net\_バッファー**は、 [**nbl**](-ndiskd-nbl.md)トピックの「例」セクションの[**net\_buffer\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)から取得されました。 NB のハンドルは ffffdf8014952610 です。

```console
2: kd> !ndiskd.nbl ffffdf80149524a0 -data
NET_BUFFER ffffdf8014952610
```

**NET\_バッファー**のハンドルをクリックするか、 **! ndiskd. nb-handle**コマンドを実行して詳細を確認できます。

```console
2: kd> !ndiskd.nb ffffdf8014952610
    NB                 ffffdf8014952610    Next NB            0
    Length             0                   Source pool        ffffdf80147e4a40
    First MDL          ffffdf8014a37930    DataOffset         0
    Current MDL        [First MDL]         Current MDL offset 0

    View associated NBL
```

**! Ndiskd nb**チェーンコマンドを使用して、その基本的な詳細に加えて、この**NET\_バッファー**の MDL チェーンを表示します。 次の例では、MDL が1つしかありません。 そのハンドルは ffffdf8014a37930 です。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワークドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd .dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-structure)

[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)

[ **!ndiskd.nbl**](-ndiskd-nbl.md)

 

 






