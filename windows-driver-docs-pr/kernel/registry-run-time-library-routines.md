---
title: レジストリ ランタイム ライブラリ ルーチン
description: レジストリ ランタイム ライブラリ ルーチン
ms.assetid: 53e55969-3c8e-44ab-8ba7-6abb0ddbfc24
keywords:
- レジストリの WDK カーネル、ランタイム ライブラリ ルーチン
- ドライバーのレジストリ情報 WDK カーネル、ランタイム ライブラリ ルーチン
- ランタイム ライブラリ ルーチンの WDK カーネル
- RtlXxxRegistryYyy ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93715ec261ff93fbc1efe758bba8ea7c4c5add8f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373454"
---
# <a name="registry-run-time-library-routines"></a>レジストリ ランタイム ライブラリ ルーチン





レジストリ エントリを操作するドライバーを呼び出すことができます、 **Rtl*Xxx*レジストリ * Xxx*** ルーチンよりシンプルなインターフェイスを提供する、 **Zw*Xxx*キー**ルーチン。 これを行うときに、ドライバーが、ハンドルを開いたり閉じたりする必要はありません。代わりに、ドライバーはキーに名前で参照します。

渡す*RelativeTo*と*パス*パラメーターをそれぞれ**Rtl*Xxx*レジストリ * Xxx*** ルーチン。 場合*RelativeTo*が右から左へ\_レジストリ\_絶対*パス*以降では、キーの完全なパスを指定します、 **\\レジストリ**ルート。 場合*RelativeTo*が右から左へ\_レジストリ\_処理、*パス*実際に開いているハンドルします。 追加 RTL\_レジストリ\_*XXX*値*RelativeTo*キーはこのような場合は、一般的なルートのパスを指定する*パス*そのルートの相対パスを指定します。 たとえば、右から左へ\_レジストリ\_ユーザーでは、する必要があります*パス*現在のユーザーのレジストリ設定を基準とします。 (この値は HKEY を指定することに相当\_現在\_ユーザー モード アプリケーションでのユーザーです)。RTL のすべての説明については\_レジストリ\_*XXX*値を参照してください[ **RtlCheckRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlcheckregistrykey)します。

次の表は、ドライバーを呼び出すことによって実行できる操作を一覧表示、 **Rtl*Xxx*レジストリ * Xxx*** ルーチン。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>操作</th>
<th>Rtl<em>Xxx</em>レジストリ<em>Xxx</em>ルーチンを呼び出す</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>レジストリ キーを作成します。</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlcreateregistrykey" data-raw-source="[&lt;strong&gt;RtlCreateRegistryKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlcreateregistrykey)"><strong>RtlCreateRegistryKey</strong></a></p></td>
</tr>
<tr class="even">
<td><p>レジストリ キーが存在するかどうかを確認します。</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlcheckregistrykey" data-raw-source="[&lt;strong&gt;RtlCheckRegistryKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlcheckregistrykey)"><strong>RtlCheckRegistryKey</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>1 つまたは複数のレジストリ キー値を確認します。</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlqueryregistryvalues" data-raw-source="[&lt;strong&gt;RtlQueryRegistryValues&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlqueryregistryvalues)"><strong>RtlQueryRegistryValues</strong></a></p></td>
</tr>
<tr class="even">
<td><p>レジストリ キー値を書き込む</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlwriteregistryvalue" data-raw-source="[&lt;strong&gt;RtlWriteRegistryValue&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlwriteregistryvalue)"><strong>RtlWriteRegistryValue</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>レジストリ キー値を削除します。</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtldeleteregistryvalue" data-raw-source="[&lt;strong&gt;RtlDeleteRegistryValue&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtldeleteregistryvalue)"><strong>RtlDeleteRegistryValue</strong></a></p></td>
</tr>
</tbody>
</table>

 

次のコード例は、設定する方法を示しています*ValueName*の **\\レジストリ\\マシン\\システム\\** <em>KeyName。</em> 0 xff の ULONG 値にします。 この例に対応する 1 つを比較、[レジストリ キー オブジェクト ルーチン](registry-key-object-routines.md)セクション。

```cpp
NTSTATUS status;
ULONG data = 0xFF;

status = RtlWriteRegistryValue(RTL_REGISTRY_ABSOLUTE,
                               (PWCSTR)L"\\Registry\\Machine\\System\\KeyName",
                               (PWCSTR)L"ValueName",
                               REG_DWORD,
                               &data,
                               sizeof(ULONG));
```

使用する場合、少数の行のコードを記述しても、 **Rtl*Xxx*レジストリ * Xxx*** ルーチンの代わりに、 **Zw*Xxx*キー**ルーチンの場合、後者のものでは、特定の操作を実行する必要があります。 たとえば、非**Rtl*Xxx*レジストリ * Xxx*** に対応するルーチンが存在する[ **ZwEnumerateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwenumeratekey)します。

同じキーに対して複数の操作を実行する場合、 **Zw*Xxx*キー**ルーチンより効率的な: 操作ごとに同じ、開いているハンドルを使用することができます。 これに対し、 **Rtl*Xxx*レジストリ * Xxx*** ルーチンが各操作に対して新しいハンドルを開いたり閉じたりします。

 

 




