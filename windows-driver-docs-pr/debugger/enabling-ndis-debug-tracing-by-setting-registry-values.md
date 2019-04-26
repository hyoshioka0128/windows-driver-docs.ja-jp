---
title: レジストリ値を設定して NDIS のデバッグのトレースを有効にする
description: レジストリ値を設定して NDIS のデバッグのトレースを有効にする
ms.assetid: ae01f546-0636-4e67-bfc7-229c3cc24b27
keywords:
- NDIS デバッグ、デバッグ、トレース、レジストリ値の設定
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d06839b09b7af4aa5c290e9d5628e7ce30a91c7e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340595"
---
# <a name="enabling-ndis-debug-tracing-by-setting-registry-values"></a>レジストリ値を設定して NDIS のデバッグのトレースを有効にする


レジストリを編集して、さまざまなレベルのさまざまな NDIS コンポーネントでのデバッグ トレースを有効にできます。 通常、次のエントリと値を追加する必要があります、 **HKLM\\システム\\CurrentControlSet\\サービス\\NDIS\\パラメーター**レジストリ キー。

```text
"DebugLevel"=dword:00000000
"DebugSystems"=dword:000030F3
"DebugBreakPoint"=dword:00000001 
```

次の値が許容される**DebugBreakPoint**、 **DebugLevel**と**DebugSystems**:

<span id="DebugBreakPoint"></span><span id="debugbreakpoint"></span><span id="DEBUGBREAKPOINT"></span>**DebugBreakPoint**  
NDIS ドライバーが、デバッガーを自動的に中断するかどうかを制御します。 NDIS のドライバーが Ndis.sys に入ったときにデバッガーに割り込むこの値が 1 に設定されている場合は**DriverEntry**関数。

<span id="DebugLevel"></span><span id="debuglevel"></span><span id="DEBUGLEVEL"></span>**DebugLevel**  
レベルとデバッグ トレースの量を選択します を選択する NDIS のコンポーネントで、 **DebugSystems**値。 次の値は、選択可能なレベルを指定します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Level</th>
<th align="left">説明</th>
<th align="left">値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DBG_LEVEL_INFO</p></td>
<td align="left"><p>すべての利用可能なデバッグ情報。 これは、最高レベルのトレースです。</p></td>
<td align="left"><p>0x00000000</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_LEVEL_LOG</p></td>
<td align="left"><p>ログ情報です。</p></td>
<td align="left"><p>0x00000800</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_LEVEL_WARN</p></td>
<td align="left"><p>警告です。</p></td>
<td align="left"><p>0x00001000</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_LEVEL_ERR</p></td>
<td align="left"><p>エラー。</p></td>
<td align="left"><p>0x00002000</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_LEVEL_FATAL</p></td>
<td align="left"><p>致命的なエラー、オペレーティング システムがクラッシュが発生することができます。 これは、トレースの最下位のレベルです。</p></td>
<td align="left"><p>0x00003000</p></td>
</tr>
</tbody>
</table>

 

<span id="DebugSystems"></span><span id="debugsystems"></span><span id="DEBUGSYSTEMS"></span>**DebugSystems**  
指定した NDIS コンポーネントのトレースのデバッグを有効にします。 これに対応を使用して、 [ **! ndiskd.dbgsystems** ](-ndiskd-dbgsystems.md)拡張機能。 次の値を選択する NDIS コンポーネントを指定します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Component</th>
<th align="left">説明</th>
<th align="left">値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DBG_COMP_INIT</p></td>
<td align="left"><p>アダプターの初期化を処理します。</p></td>
<td align="left"><p>0x00000001</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_CONFIG</p></td>
<td align="left"><p>アダプターの構成を処理します。</p></td>
<td align="left"><p>0x00000002</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_SEND</p></td>
<td align="left"><p>ネットワーク経由でデータの送信を処理します。</p></td>
<td align="left"><p>0x00000004</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_RECV</p></td>
<td align="left"><p>ネットワークからデータを受け取って処理します。</p></td>
<td align="left"><p>0x00000008</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_PROTOCOL</p></td>
<td align="left"><p>プロトコル操作を処理します。</p></td>
<td align="left"><p>0x00000010</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_BIND</p></td>
<td align="left"><p>バインディング操作を処理します。</p></td>
<td align="left"><p>0x00000020</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_BUSINFO</p></td>
<td align="left"><p>バスのクエリを処理します。</p></td>
<td align="left"><p>0x00000040</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_REG</p></td>
<td align="left"><p>レジストリの操作を処理します。</p></td>
<td align="left"><p>0x00000080</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_MEMORY</p></td>
<td align="left"><p>メモリ管理を処理します。</p></td>
<td align="left"><p>0x00000100</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_FILTER</p></td>
<td align="left"><p>ハンドルは、操作をフィルター処理します。</p></td>
<td align="left"><p>0x00000200</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_REQUEST</p></td>
<td align="left"><p>要求を処理します。</p></td>
<td align="left"><p>0x00000400</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_WORK_ITEM</p></td>
<td align="left"><p>作業項目の操作のハンドル</p></td>
<td align="left"><p>0x00000800</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_PNP</p></td>
<td align="left"><p>プラグ アンド プレイの操作を処理します。</p></td>
<td align="left"><p>0x00001000</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_PM</p></td>
<td align="left"><p>電源管理操作を処理します。</p></td>
<td align="left"><p>0x00002000</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_OPENREF</p></td>
<td align="left"><p>参照オブジェクトを開く操作を処理します。</p></td>
<td align="left"><p>0x00004000</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_LOCKS</p></td>
<td align="left"><p>ロック操作を処理します。</p></td>
<td align="left"><p>0x00008000</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_RESET</p></td>
<td align="left"><p>リセット操作を処理します。</p></td>
<td align="left"><p>0x00010000</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_WMI</p></td>
<td align="left"><p>Windows Management Instrumentation の操作を処理します。</p></td>
<td align="left"><p>0x00020000</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_CO</p></td>
<td align="left"><p>接続指向の NDIS を処理します。</p></td>
<td align="left"><p>0x00040000</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_REF</p></td>
<td align="left"><p>ハンドルは、操作を参照します。</p></td>
<td align="left"><p>0x00080000</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_ALL</p></td>
<td align="left"><p>NDIS のすべてのコンポーネントを処理します。</p></td>
<td align="left"><p>0 xffffffff</p></td>
</tr>
</tbody>
</table>

 

1 つ以上の NDIS コンポーネントを選択できます。 1 つ以上のコンポーネントが選択されている場合は、OR 演算子を伴うデータ値を結合します。 たとえば、DBG を選択する\_COMP\_PNP、DBG\_COMP\_PM、DBG\_COMP\_INIT と DBG\_COMP\_構成では、対応する結合が値 (0x1000、0x2000、0x1 と 0x2) 0x3003、値を取得し、そのため、レジストリに設定する:

```text
"DebugSystems"=dword:00003003
```

デバッグ トレースのレジストリ値を変更するたびに、新しい設定を有効にするには、コンピューターを再起動する必要があります。

 

 





