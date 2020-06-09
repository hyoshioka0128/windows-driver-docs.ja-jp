---
title: ndiskd ndisslot
description: '**! Ndiskd ndisslot**拡張機能は、プロセッサごとの NDIS 変数の内容を表示します。'
ms.assetid: 0EF37FE7-31A1-4A71-9CAC-E2A43F0EEBCF
keywords:
- ndisslot Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.ndisslot
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c4fa2bd992156e6d2e8bc40550d68f763d84527c
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534917"
---
# <a name="ndiskdndisslot"></a>!ndiskd.ndisslot


**メモ**   サードパーティのネットワークドライバーの開発者は、この拡張機能コマンドを手動で使用することは想定されていません。 これを実行すると表示される情報を確認できますが、ドライバーで提供される詳細を再利用することはできません。

 

**! Ndiskd ndisslot**拡張機能は、プロセッサごとの NDIS 変数の内容を表示します。 パラメーターを使用せずにこの拡張機能を実行すると、システム上のプロセッサごとのすべての NDIS 変数の一覧が表示されます。

```console
!ndiskd.ndisslot [-handle <x>] [-itemtype <str>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-ハンドル*   
スロットのハンドル。

<span id="_______-itemtype______"></span><span id="_______-ITEMTYPE______"></span>*-itemtype*   
スロットに格納されている値の型。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

<a name="examples"></a>例
--------

パラメーターを使用せずに **! ndiskd ndisslot**拡張機能を実行すると、プロセッサごとのすべてのスロット変数の一覧が表示されます。 次の出力例では、簡潔にするためにリストの中間部分を excised しています。

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

プロセッサごとのスロット変数のハンドルの1つをクリックすると、その変数の詳細が表示されます。 次の例では、前の例の tsR 変数にハンドル ffffc804ae060920 を使用しています。

```console
1: kd> !ndiskd.ndisslot ffffc804ae060920
    Processor          Slot value                                               
    00                 00000006
    01                 00000006
    02                 00000006
    03                 00000006
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワーク ドライバー設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 拡張機能 (Ndiskd .dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

 

 






