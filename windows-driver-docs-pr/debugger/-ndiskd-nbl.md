---
title: ndiskd.nbl
description: Ndiskd.nbl 拡張機能では、NET_BUFFER_LIST (NBL) 構造に関する情報が表示されます。
ms.assetid: 1806ac7c-b438-4c28-bab0-1b65dba651ea
keywords:
- デバッグ ndiskd.nbl Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.nbl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d57373ebf44c4b95c91323b053f5aa997758b9ae
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364276"
---
# <a name="ndiskdnbl"></a>!ndiskd.nbl


**! Ndiskd.nbl**拡張機能に関する情報を表示する、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure) (NBL) 構造体。

```console
    !ndiskd.nbl [-handle <x>] [-basic] [-chain] [-info] [-data] 
    [-netmon] [-capfile <str>] [-launch] [-overwrite] [-log]
    [-stacks] [-NblCurrentOwner]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必須。 アドレスを**NET\_バッファー\_一覧**構造体。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span> *-basic*   
NBL、に関する基本的な情報が表示されます。

<span id="_______-chain______"></span><span id="_______-CHAIN______"></span> *チェーン*   
すべての NBLs が表示されますおよび[ **NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-structure)NBL、チェーン内。

<span id="_______-info______"></span><span id="_______-INFO______"></span> *-情報*   
NBL に関連付けられているすべての帯域外の情報が表示されます。

<span id="_______-data______"></span><span id="_______-DATA______"></span> *-data*   
NBL の実際のデータ ペイロードを表示します。

<span id="_______-netmon______"></span><span id="_______-NETMON______"></span> *-netmon*   
Microsoft Network monitor NBL チェーンを表示します。

<span id="_______-capfile______"></span><span id="_______-CAPFILE______"></span> *-capfile*   
Netmon キャプチャの保存先のパスを指定します。

<span id="_______-launch______"></span><span id="_______-LAUNCH______"></span> *-launch*   
キャプチャ ファイルを保存した後、netmon.exe を自動的に起動します。

<span id="_______-overwrite______"></span><span id="_______-OVERWRITE______"></span> *-overwrite*   
既に存在する場合は、キャプチャ ファイルを上書きできます。

<span id="_______-log______"></span><span id="_______-LOG______"></span> *-log*   
NBL ログ NBL 履歴ログが有効になっているかどうかを示しています。

<span id="_______-stacks______"></span><span id="_______-STACKS______"></span> *-履歴*   
NBL ログ (ログで使用) で呼び出し履歴が含まれています。

<span id="_______-NblCurrentOwner______"></span><span id="_______-nblcurrentowner______"></span><span id="_______-NBLCURRENTOWNER______"></span> *-NblCurrentOwner*   
NBL の現在の所有者を示しています。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>使用例
--------

次の例では、NBL の追跡が有効になって、NBL NBL ログからのハンドルを抽出します。 NBL の追跡と NBL ログの詳細については、次を参照してください。 [ **! ndiskd.nbllog**](-ndiskd-nbllog.md)します。

ログの収集時に、この例では NBL が WFP ネイティブ Mac レイヤー ライトウェイト フィルターに TCPIP6 プロトコルによって返されました。

```console
2: kd> !ndiskd.nbl ffffdf80149524a0
    NBL                ffffdf80149524a0    Next NBL           NULL
    First NB           ffffdf8014952610    Source             ffffdf80140c71a0 - Microsoft Kernel Debug Network Adapter
    Flags              INDICATED, RETURNED, NBL_ALLOCATED, PROTOCOL_020_0,
                       PROTOCOL_200_0

    Walk the NBL chain                     Dump data payload
    Show out-of-band information
    Review NBL history
```

入力することも、前の例「のデータ ペイロードをダンプする」リンクをクリックして、 **! ndiskd.nbl-データの処理 -** コマンドをこの NBL のデータ ペイロードを確認できます。 次の例では、NBL を含む 1 つだけ**NET\_バッファー**構造体。 さらにその内容を表示する**NET\_バッファー**構造、実行、 [ **! ndiskd.nb-処理**](-ndiskd-nb.md)そのハンドルを持つコマンド。

```console
2: kd> !ndiskd.nbl ffffdf80149524a0 -data
NET_BUFFER ffffdf8014952610
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

[**NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)

[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-structure)

[ **!ndiskd.nbllog**](-ndiskd-nbllog.md)

[ **!ndiskd.nb**](-ndiskd-nb.md)

 

 






