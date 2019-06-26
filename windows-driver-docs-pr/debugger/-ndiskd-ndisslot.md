---
title: ndiskd.ndisslot
description: '**! Ndiskd.ndisslot**拡張機能は、NDIS、プロセッサごとの変数の内容を表示します。'
ms.assetid: 0EF37FE7-31A1-4A71-9CAC-E2A43F0EEBCF
keywords:
- デバッグ ndiskd.ndisslot Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.ndisslot
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0b9ff3e98b774209d12f03da700967ce23dc6c6f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363133"
---
# <a name="ndiskdndisslot"></a>!ndiskd.ndisslot


**注**  サード パーティ製ネットワーク ドライバー開発者が手動でこの拡張機能のコマンドを使用する必要はありません。 表示される情報を表示することを行うことができますが、ドライバー、詳細を再利用できません。

 

**! Ndiskd.ndisslot**拡張機能は、NDIS、プロセッサごとの変数の内容を表示します。 パラメーターなしで、この拡張機能を実行する場合。 ndiskd は、システム上で NDIS、プロセッサごとのすべての変数の一覧を表示します。

```console
!ndiskd.ndisslot [-handle <x>] [-itemtype <str>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
スロットのハンドル。

<span id="_______-itemtype______"></span><span id="_______-ITEMTYPE______"></span> *-itemtype*   
スロットに格納されている値の型。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>例
--------

実行、 **! ndiskd.ndisslot**プロセッサあたりのスロットのすべての変数の一覧を表示するパラメーターなしで拡張機能。 次の出力例は、簡潔にするためのリストの中央部分に excised が。

```console
1: kd> !ndiskd.ndisslot
    Per-processor slot                     Summary of contents                  
    ffffc804ae060000 - NDrw                All values are zero
    ffffc804ae060008 - NDrw                All values are zero
    ffffc804ae060010 - NDrw                All values are zero
    ffffc804ae060018 - NDrw                All values are zero
    ffffc804ae060020 - NDrw                All values are zero
    ffffc804ae060028 - NDrw                All values are zero
    ffffc804ae060030 - NDrw                All values are zero
    ffffc804ae060038 - NDrw                All values are zero
    ffffc804ae060040 - NDrw                All values are zero
    ffffc804ae060048 - NDrw                All values are zero

...

    ffffc804ae060910 - NDtk                All values are zero
    ffffc804ae060918 - NDtk                All values are zero
    ffffc804ae060920 - tsR                 All values are non-zero
    ffffc804ae060928 - NDrw                All values are zero
    ffffc804ae060930 - NDtk                All values are zero
    ffffc804ae060938 - NDtk                All values are zero
    ffffc804ae060940 - NDtk                All values are zero
    ffffc804ae060948 - NDtk                All values are zero
    ffffc804ae060950 - NDrw                All values are zero
    ffffc804ae060958 - NDrw                All values are zero

    Statistics
    Descriptors        1
    Total slots        512
    Slots available    275
    Slots used         237
    Efficiency         46%
```

プロセッサあたりのスロットの変数のハンドルのいずれかをクリックすると詳細が表示 変数。 次の例では、前の例から、tsR 変数のハンドル ffffc804ae060920 を使用します。

```console
1: kd> !ndiskd.ndisslot ffffc804ae060920
    Processor          Slot value                                               
    00                 00000006
    01                 00000006
    02                 00000006
    03                 00000006
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

 

 






