---
title: NDIS のデバッグのトレースを有効にする
description: NDIS のデバッグのトレースを有効にする
ms.assetid: 4ca3c246-3e73-46fb-93a5-ea376788e330
keywords:
- NDIS デバッグ、デバッグトレース
ms.date: 05/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: 2d8beecd2553692053b4bbbe38d12158a080d25b
ms.sourcegitcommit: 8596782b07c8a71adf38fc2c2da68b75ba0a1259
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85593968"
---
# <a name="enabling-ndis-debug-tracing"></a>NDIS のデバッグのトレースを有効にする

Ndis デバッグトレースは、NDIS ドライバーをデバッグするための主要な方法です。 NDIS デバッグトレースを設定するときに、実際には、NDIS で1つ以上のレベルの DbgPrint ステートメントを有効にします。 結果として得られる情報は、ほとんどのネットワークドライバーの問題をデバッグするのに十分です。

## <a name="enabling-ndis-debug-tracing-by-setting-registry-values"></a>レジストリ値を設定して NDIS のデバッグのトレースを有効にする

レジストリを編集することで、さまざまな NDIS コンポーネントでさまざまなレベルのデバッグトレースを有効にすることができます。 通常は、次のエントリと値を**HKLM \\ SYSTEM \\ CurrentControlSet \\ Services \\ NDIS \\ Parameters**レジストリキーに追加する必要があります。

```text
"DebugLevel"=dword:00000000
"DebugSystems"=dword:000030F3
"DebugBreakPoint"=dword:00000001 
```

**Debugbreakpoint ポイント**、 **debugbreakpoint** 、および**debugbreakpoint**では、次の値を使用できます。

<span id="DebugBreakPoint"></span><span id="debugbreakpoint"></span><span id="DEBUGBREAKPOINT"></span>**DebugBreakPoint ポイント**  
NDIS ドライバーが自動的にデバッガーに中断するかどうかを制御します。 この値が1に設定されている場合、NDIS は、ドライバーが Ndis.sys の**Driverentry**関数に入ったときにデバッガーを中断します。

<span id="DebugLevel"></span><span id="debuglevel"></span><span id="DEBUGLEVEL"></span>**DebugLevel**  
**Debugsystems**値を使用して選択した NDIS コンポーネント内のデバッグトレースのレベルまたは量を選択します。 次の値は、選択できるレベルを指定します。

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
<td align="left"><p>使用可能なすべてのデバッグ情報。 これは、最も高いレベルのトレースです。</p></td>
<td align="left"><p>0x00000000</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_LEVEL_LOG</p></td>
<td align="left"><p>ログ情報。</p></td>
<td align="left"><p>0x00000800</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_LEVEL_WARN</p></td>
<td align="left"><p>[警告]。</p></td>
<td align="left"><p>0x00001000</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_LEVEL_ERR</p></td>
<td align="left"><p>エラー。</p></td>
<td align="left"><p>0x00002000</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_LEVEL_FATAL</p></td>
<td align="left"><p>致命的なエラーが発生すると、オペレーティングシステムがクラッシュする可能性があります。 これは、トレースの最下位レベルです。</p></td>
<td align="left"><p>0x00003000</p></td>
</tr>
</tbody>
</table>

<span id="DebugSystems"></span><span id="debugsystems"></span><span id="DEBUGSYSTEMS"></span>**DebugSystems**  
指定された NDIS コンポーネントのデバッグトレースを有効にします。 これは、 [**! ndiskd dbgsystems**](-ndiskd-dbgsystems.md)拡張機能の使用に対応しています。 次の値によって、選択できる NDIS コンポーネントが指定されます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コンポーネント</th>
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
<td align="left"><p>アダプター構成を処理します。</p></td>
<td align="left"><p>0x00000002</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_SEND</p></td>
<td align="left"><p>ネットワーク経由でのデータ送信を処理します。</p></td>
<td align="left"><p>0x00000004</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_RECV</p></td>
<td align="left"><p>ネットワークからのデータの受信を処理します。</p></td>
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
<td align="left"><p>バスクエリを処理します。</p></td>
<td align="left"><p>0x00000040</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_REG</p></td>
<td align="left"><p>レジストリ操作を処理します。</p></td>
<td align="left"><p>0x00000080</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_MEMORY</p></td>
<td align="left"><p>メモリ管理を処理します。</p></td>
<td align="left"><p>0x00000100</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_FILTER</p></td>
<td align="left"><p>フィルター操作を処理します。</p></td>
<td align="left"><p>0x00000200</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_REQUEST</p></td>
<td align="left"><p>要求を処理します。</p></td>
<td align="left"><p>0x00000400</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_WORK_ITEM</p></td>
<td align="left"><p>作業項目の操作を処理します。</p></td>
<td align="left"><p>0x00000800</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_PNP</p></td>
<td align="left"><p>プラグアンドプレイ操作を処理します。</p></td>
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
<td align="left"><p>Windows Management Instrumentation 操作を処理します。</p></td>
<td align="left"><p>0x00020000</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_CO</p></td>
<td align="left"><p>接続指向の NDIS を処理します。</p></td>
<td align="left"><p>0x00040000</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMP_REF</p></td>
<td align="left"><p>参照操作を処理します。</p></td>
<td align="left"><p>0x00080000</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_COMP_ALL</p></td>
<td align="left"><p>すべての NDIS コンポーネントを処理します。</p></td>
<td align="left"><p>~</p></td>
</tr>
</tbody>
</table>

複数の NDIS コンポーネントを選択できます。 複数のコンポーネントが選択されている場合は、データ値を OR 演算子で結合します。 たとえば、DBG \_ カンプ \_ 、dbg comp PM、dbg comp INIT、dbg comp CONFIG を選択するには、 \_ 対応する \_ \_ \_ \_ \_ 値 (0x1000、0x2000、0x1、0x2) を組み合わせて、値0x3003 を取得し、次のようにレジストリに設定します。

```text
"DebugSystems"=dword:00003003
```

デバッグトレースのレジストリ値を変更するときは常に、新しい設定を有効にするためにコンピューターを再起動する必要があります。
