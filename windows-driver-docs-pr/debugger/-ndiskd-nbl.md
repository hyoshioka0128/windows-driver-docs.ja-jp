---
title: ndiskd nbl
description: Nbl 拡張機能には、NET_BUFFER_LIST (NBL) 構造に関する情報が表示されます。
ms.assetid: 1806ac7c-b438-4c28-bab0-1b65dba651ea
keywords:
- nbl Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.nbl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b332cc716c87072a70503682eede88962a54d808
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837587"
---
# <a name="ndiskdnbl"></a>!ndiskd.nbl


**! Ndiskd**拡張機能には、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure) (nbl) 構造に関する情報が表示されます。

```console
    !ndiskd.nbl [-handle <x>] [-basic] [-chain] [-info] [-data] 
    [-netmon] [-capfile <str>] [-launch] [-overwrite] [-log]
    [-stacks] [-NblCurrentOwner]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-  を処理*します  
必須。 **NET\_BUFFER\_LIST**構造体のアドレス。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span> *-基本*   
NBL に関する基本的な情報を表示します。

<span id="_______-chain______"></span><span id="_______-CHAIN______"></span> *-チェーン*   
NBLs と[**NET\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-structure)のすべてのバッファーを NBL チェーンに表示します。

<span id="_______-info______"></span><span id="_______-INFO______"></span> *-info*   
NBL に関連付けられているすべての帯域外情報を表示します。

<span id="_______-data______"></span><span id="_______-DATA______"></span> *-データ*   
NBL の実際のデータペイロードを表示します。

<span id="_______-netmon______"></span><span id="_______-NETMON______"></span> *-netmon*   
Microsoft ネットワークモニターの NBL チェーンを表示します。

<span id="_______-capfile______"></span><span id="_______-CAPFILE______"></span> *-capfile*   
Netmon キャプチャを保存するパスを指定します。

<span id="_______-launch______"></span><span id="_______-LAUNCH______"></span> *-  を起動*します  
キャプチャファイルを保存した後、netmon を自動的に起動します。

<span id="_______-overwrite______"></span><span id="_______-OVERWRITE______"></span> *-上書き*   
キャプチャファイルが既に存在する場合は上書きできます。

<span id="_______-log______"></span><span id="_______-LOG______"></span> *-log*   
NBL 履歴ログが有効になっている場合は、NBL log を表示します。

<span id="_______-stacks______"></span><span id="_______-STACKS______"></span> *-スタック*   
呼び出し履歴 with NBL log (-log を使用した) が含まれます。

<span id="_______-NblCurrentOwner______"></span><span id="_______-nblcurrentowner______"></span><span id="_______-NBLCURRENTOWNER______"></span> *-NblCurrentOwner*   
NBL の現在の所有者を表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

<a name="examples"></a>例
--------

次の例では、NBL ログから NBL のハンドルを抽出するために、NBL tracking が有効になっています。 NBL tracking と NBL ログの詳細については、「 [ **! ndiskd ndiskd**](-ndiskd-nbllog.md)」を参照してください。

ログ収集時に、この例の NBL が TCPIP6 プロトコルによって WFP ネイティブ Mac レイヤーライトウェイトフィルターに返されました。

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

前の例の "Dump data payload" リンクをクリックするか、 **! ndiskd**コマンドを入力して、この nbl のデータペイロードを確認することができます。 次の例では、NBL に含まれるのは、1つの**NET\_バッファー**構造体だけです。 その**NET\_のバッファー**構造の内容をさらに詳しく調べるには、 [ **! ndiskd. nb-handle**](-ndiskd-nb.md)コマンドをハンドルと共に実行します。

```console
2: kd> !ndiskd.nbl ffffdf80149524a0 -data
NET_BUFFER ffffdf8014952610
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワークドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd .dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)

[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-structure)

[ **!ndiskd.nbllog**](-ndiskd-nbllog.md)

[ **!ndiskd.nb**](-ndiskd-nb.md)

 

 






