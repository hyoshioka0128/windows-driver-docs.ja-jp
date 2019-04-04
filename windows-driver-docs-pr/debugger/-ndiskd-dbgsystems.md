---
title: ndiskd.dbgsystems
description: Ndiskd.dbgsystems 拡張機能では、表示し、必要に応じてデバッグ トレースを有効になっている NDIS サブシステムを変更します。  ndiskd.dbgsystems は、WPP とドライバーの検証ツールが提供されています。
ms.assetid: f36a26b6-18a8-4a01-96c7-99826e6b662f
keywords:
- デバッグ ndiskd.dbgsystems Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.dbgsystems
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 56354f8347201c637191318919efa66508bec642
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530070"
---
# <a name="ndiskddbgsystems"></a>!ndiskd.dbgsystems


**! Ndiskd.dbgsystems**拡張機能が表示され、必要に応じてデバッグ トレースを有効になっている NDIS サブシステムを変更します。

**警告**  
 **! ndiskd.dbgsystems** WPP (Windows ソフトウェア トレース プリプロセッサ) とドライバーの検証ツールが提供されています。 ! ndiskd が表示されます、次の警告、ターゲット システムがサポートされていない場合 **! ndiskd.dbgsystems**します。

```console
0: kd> !ndiskd.dbgsystems
    This target does not support tracing through !ndiskd.dbglevel or
    !ndiskd.dbgsystems.
    Learn how to collect traces with WPP
```

場合は、警告の下部にあるリンクをクリックします。 ndiskd が詳細情報を提供します。

```console
0: kd> !ndiskd.help wpptracing
    WPP traces are fast, flexible, and detailed.  Plus, starting with Windows 8
    and Windows Server 2012, you can automatically decode NDIS traces using the
    symbol file.  Just point TraceView (or tracepdb.exe) at NDIS.PDB, and it
    will be able to get all the TMFs it needs to trace NDIS activity.
    
    If you would like traces to be printed in the debugger window, you use the
    !wmitrace extension.  For example, you might enable traces with this:

    !wmitrace.searchpath c:\path\to\TMF\files
    !wmitrace.start ndis -kd
    !wmitrace.enable ndis {DD7A21E6-A651-46D4-B7C2-66543067B869} -level 4 -flag 0x31f3
```

 

詳細については、WPP は、[WPP ソフトウェア トレース](https://msdn.microsoft.com/windows/hardware/drivers/devtest/wpp-software-tracing)を参照してください。

Driver Verifier についての詳細については、[Driver Verifier](https://msdn.microsoft.com/windows/hardware/drivers/devtest/driver-verifier)を参照してください。

WMI のトレースの詳細については、[WMI トレース拡張機能 (Wmitrace.dll)](https://msdn.microsoft.com/library/windows/hardware/ff561362)を参照してください。

```console
!ndiskd.dbgsystems [-subsystem <any>] 
```

## <a name="span-idddkndiskddbgsystemsdbgspanspan-idddkndiskddbgsystemsdbgspanparameters"></a><span id="ddk__ndiskd_dbgsystems_dbg"></span><span id="DDK__NDISKD_DBGSYSTEMS_DBG"></span>パラメーター


<span id="_______-subsystem______"></span><span id="_______-SUBSYSTEM______"></span> *-subsystem*   
切り替えるサブシステムです。

複数のコンポーネントが選択されている場合は、空白で区切ります。 以前に選択されたコンポーネントが繰り返し発生する場合オフ デバッグ監視が切り替えるされます。 可能な値は次のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>値</strong></p></td>
<td align="left"><p><strong>意味</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>INIT</p></td>
<td align="left"><p>アダプターの初期化をトレースします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>構成</p></td>
<td align="left"><p>アダプターの構成をトレースします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>送信</p></td>
<td align="left"><p>トレースは、ネットワーク経由でデータを送信します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RECV</p></td>
<td align="left"><p>トレースは、ネットワークからデータを受信します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>プロトコル</p></td>
<td align="left"><p>プロトコル操作をトレースします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>バインド</p></td>
<td align="left"><p>バインディング操作をトレースします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>BUS_QUERY</p></td>
<td align="left"><p>バスのクエリをトレースします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>レジストリ</p></td>
<td align="left"><p>レジストリの操作をトレースします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>メモリ</p></td>
<td align="left"><p>メモリ管理をトレースします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>フィルター</p></td>
<td align="left"><p>トレースは、操作をフィルター処理します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>要求</p></td>
<td align="left"><p>要求をトレースします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WORK_ITEM</p></td>
<td align="left"><p>作業項目の操作のトレース</p></td>
</tr>
<tr class="even">
<td align="left"><p>PNP</p></td>
<td align="left"><p>プラグ アンド プレイの操作をトレースします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PM</p></td>
<td align="left"><p>電源管理操作をトレースします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>開いています。</p></td>
<td align="left"><p>参照オブジェクトを開く操作をトレースします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ロック</p></td>
<td align="left"><p>ロック操作をトレースします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>リセット</p></td>
<td align="left"><p>トレースの操作をリセットします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WMI に関するページ</p></td>
<td align="left"><p>Windows Management Instrumentation の操作をトレースします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NDIS_CO</p></td>
<td align="left"><p>接続指向 NDIS をトレースします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>参照</p></td>
<td align="left"><p>トレースは、操作を参照します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="remarks"></a>注釈
-------

この拡張機能は、checked NDIS.sys のみに適用されます。 NDIS.sys のビルド情報を確認するには、実行、 [ **! ndiskd.ndis** ](-ndiskd-ndis.md)拡張機能。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**!ndiskd.ndis**](-ndiskd-ndis.md)

[WPP ソフトウェア トレース](https://msdn.microsoft.com/windows/hardware/drivers/devtest/wpp-software-tracing)

[Driver Verifier](https://msdn.microsoft.com/windows/hardware/drivers/devtest/driver-verifier)

[WMI 拡張機能 (Wmitrace.dll) のトレース](https://msdn.microsoft.com/library/windows/hardware/ff561362)

 

 






