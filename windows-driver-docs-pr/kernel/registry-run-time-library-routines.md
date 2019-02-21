---
title: レジストリのランタイム ライブラリ ルーチン
description: レジストリのランタイム ライブラリ ルーチン
ms.assetid: 53e55969-3c8e-44ab-8ba7-6abb0ddbfc24
keywords:
- レジストリの WDK カーネル、ランタイム ライブラリ ルーチン
- ドライバーのレジストリ情報 WDK カーネル、ランタイム ライブラリ ルーチン
- ランタイム ライブラリ ルーチンの WDK カーネル
- RtlXxxRegistryYyy ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 759770a949541de488c13fcc39d021568ab3e0bb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549246"
---
# <a name="registry-run-time-library-routines"></a>レジストリのランタイム ライブラリ ルーチン





レジストリ エントリを操作するドライバーを呼び出すことができます、 **Rtl*Xxx*レジストリ * Xxx*** ルーチンよりシンプルなインターフェイスを提供する、 **Zw*Xxx*キー**ルーチン。 これを行うときに、ドライバーが、ハンドルを開いたり閉じたりする必要はありません。代わりに、ドライバーはキーに名前で参照します。

渡す*RelativeTo*と*パス*パラメーターをそれぞれ**Rtl*Xxx*レジストリ * Xxx*** ルーチン。 場合*RelativeTo*が右から左へ\_レジストリ\_絶対*パス*以降では、キーの完全なパスを指定します、 **\\レジストリ**ルート。 場合*RelativeTo*が右から左へ\_レジストリ\_処理、*パス*実際に開いているハンドルします。 追加 RTL\_レジストリ\_*XXX*値*RelativeTo*キーはこのような場合は、一般的なルートのパスを指定する*パス*そのルートの相対パスを指定します。 たとえば、右から左へ\_レジストリ\_ユーザーでは、する必要があります*パス*現在のユーザーのレジストリ設定を基準とします。 (この値は HKEY を指定することに相当\_現在\_ユーザー モード アプリケーションでのユーザーです)。RTL のすべての説明については\_レジストリ\_*XXX*値を参照してください[ **RtlCheckRegistryKey**](https://msdn.microsoft.com/library/windows/hardware/ff561754)します。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561822" data-raw-source="[&lt;strong&gt;RtlCreateRegistryKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561822)"><strong>RtlCreateRegistryKey</strong></a></p></td>
</tr>
<tr class="even">
<td><p>レジストリ キーが存在するかどうかを確認します。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561754" data-raw-source="[&lt;strong&gt;RtlCheckRegistryKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561754)"><strong>RtlCheckRegistryKey</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>1 つまたは複数のレジストリ キー値を確認します。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562046" data-raw-source="[&lt;strong&gt;RtlQueryRegistryValues&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562046)"><strong>RtlQueryRegistryValues</strong></a></p></td>
</tr>
<tr class="even">
<td><p>レジストリ キー値を書き込む</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563034" data-raw-source="[&lt;strong&gt;RtlWriteRegistryValue&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563034)"><strong>RtlWriteRegistryValue</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>レジストリ キー値を削除します。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561829" data-raw-source="[&lt;strong&gt;RtlDeleteRegistryValue&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561829)"><strong>RtlDeleteRegistryValue</strong></a></p></td>
</tr>
</tbody>
</table>

 

次のコード例は、設定する方法を示しています*ValueName*の**\\レジストリ\\マシン\\システム\\**<em>KeyName。</em> 0 xff の ULONG 値にします。 この例に対応する 1 つを比較、[レジストリ キー オブジェクト ルーチン](registry-key-object-routines.md)セクション。

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

使用する場合、少数の行のコードを記述しても、 **Rtl*Xxx*レジストリ * Xxx*** ルーチンの代わりに、 **Zw*Xxx*キー**ルーチンの場合、後者のものでは、特定の操作を実行する必要があります。 たとえば、非**Rtl*Xxx*レジストリ * Xxx*** に対応するルーチンが存在する[ **ZwEnumerateKey**](https://msdn.microsoft.com/library/windows/hardware/ff566447)します。

同じキーに対して複数の操作を実行する場合、 **Zw*Xxx*キー**ルーチンより効率的な: 操作ごとに同じ、開いているハンドルを使用することができます。 これに対し、 **Rtl*Xxx*レジストリ * Xxx*** ルーチンが各操作に対して新しいハンドルを開いたり閉じたりします。

 

 




