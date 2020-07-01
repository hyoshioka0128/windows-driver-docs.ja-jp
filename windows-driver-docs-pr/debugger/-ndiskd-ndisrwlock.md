---
title: ndiskd ndisrwlock
description: Ndisrwlock 拡張機能には、NDIS_RW_LOCK_EX ロック構造に関する情報が表示されます。
ms.assetid: 853CBAFE-3899-4983-BFC7-933D3BC7ADA1
keywords:
- ndisrwlock Windows デバッグ
ms.date: 06/18/2020
topic_type:
- apiref
api_name:
- ndiskd.ndisrwlock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6ce40c0652d57e6a941f19bc1f99e7673cb92bbb
ms.sourcegitcommit: 8596782b07c8a71adf38fc2c2da68b75ba0a1259
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85593924"
---
# <a name="ndiskdndisrwlock"></a>!ndiskd.ndisrwlock

**! Ndiskd ndisrwlock**拡張機能には、 [**NDIS \_ RW \_ lock \_ EX**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff567279(v=vs.85)) lock 構造体に関する情報が表示されます。

```console
!ndiskd.ndisrwlock -handle <x>
```

## <a name="parameters"></a>パラメーター

<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-ハンドル*   
必須。 ロック構造体のハンドル。

### <a name="dll"></a>[DLL]

Ndiskd.dll

### <a name="examples"></a>例

独自の RW ロックを作成し、それを検査する場合は、 **! ndiskd ndisrwlock**拡張機能を使用します。 RW ロックのハンドルを取得するには、 *poi*コマンドを使用して、ドライバーのロックのアドレスを逆参照します。 次のスニペットは、この例の時点で TCIPIP プロトコルが使用していたロックを確認する方法を示しています。

```console
0: kd> !ndiskd.ndisrwlock poi(tcpip!gAleHashtableLock)


NDIS READ-WRITE LOCK

    Allocated by       [NDIS generic object]
    Exclusive access   Not acquired
    Read-only access   0 references

    Set a breakpoint on acquire/release
```

この RW ロックを使用してドライバーを観察するには、RW ロックの詳細の下部にある [取得/解放時にブレークポイントを設定する] リンクをクリックします。 ブレークポイントを設定した後、 **g**コマンドを入力して、デバッグ対象マシンを実行し、ブレークポイントにヒットします。

```console
0: kd> ba r4 ffffe00bc3fc22f8
0: kd> g
Breakpoint 0 hit
nt!KeTestSpinLock+0x3:
fffff802`0d69eb53 4885c0          test    rax,rax
```

これで、同じ **! ndiskd**コマンドを再実行して、この RW ロックに読み取り専用アクセスの参照が1つあることを確認できます。

```console
0: kd> !ndiskd.ndisrwlock poi(tcpip!gAleHashtableLock)


NDIS READ-WRITE LOCK

    Allocated by       [NDIS generic object]
    Exclusive access   Not acquired
    Read-only access   1 reference

    Set a breakpoint on acquire/release
```

## <a name="see-also"></a>関連項目

[ネットワーク ドライバー設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**NDIS \_ RW \_ LOCK \_ EX**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff567279(v=vs.85))
