---
title: レジストリ ランタイム ライブラリ ルーチン
description: レジストリ ランタイム ライブラリ ルーチン
ms.assetid: 53e55969-3c8e-44ab-8ba7-6abb0ddbfc24
keywords:
- レジストリ WDK カーネル、ランタイムライブラリルーチン
- ドライバーレジストリ情報 WDK カーネル、ランタイムライブラリルーチン
- ランタイムライブラリルーチン WDK カーネル
- RtlXxxRegistryYyy ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2369bc67424e3052c3cc6065e23186b763c1a8d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827460"
---
# <a name="registry-run-time-library-routines"></a>レジストリ ランタイム ライブラリ ルーチン





レジストリエントリを操作するために、ドライバーは**Rtl*xxx*レジストリ * Xxx*** ルーチンを呼び出すことができます。これにより、 **Zw*xxx*キー**ルーチンよりも簡単なインターフェイスが提供されます。 この場合、ハンドルを開いたり閉じたりする必要はありません。代わりに、ドライバーは名前でキーを参照します。

各**Rtl*Xxx*Registry * Xxx*** ルーチンに*RelativeTo*および*Path*パラメーターを渡します。 *RelativeTo*が RTL\_REGISTRY\_ABSOLUTE の場合、 *Path*は **\\レジストリ**ルートで始まるキーの完全なパスを指定します。 *RelativeTo*が RTL\_REGISTRY\_ハンドルの場合、*パス*は実際には開いているハンドルです。 *RelativeTo*の追加の RTL\_レジストリ\_*XXX*の値は、キーの共通ルートのパスを指定します。このような場合、 *path*はそのルートを基準とした相対パスを指定します。 たとえば、RTL\_REGISTRY\_ユーザーは、現在のユーザーのレジストリ設定に対する相対*パス*である必要があります。 (この値は、ユーザーモードアプリケーションで現在\_ユーザー\_HKEY を指定することと同じです)。すべての RTL\_REGISTRY\_*XXX*値の詳細については、「 [**Rtlcheckregistrykey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlcheckregistrykey)」を参照してください。

次の表に、 **Rtl*Xxx*レジストリ * Xxx*** ルーチンを呼び出すことによってドライバーが実行できる操作を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>操作</th>
<th>Rtl<em>xxx</em>Registry<em>xxx</em>ルーチンの呼び出し</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>レジストリキーを作成する</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlcreateregistrykey" data-raw-source="[&lt;strong&gt;RtlCreateRegistryKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlcreateregistrykey)"><strong>RtlCreateRegistryKey</strong></a></p></td>
</tr>
<tr class="even">
<td><p>レジストリキーが存在するかどうかを確認する</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlcheckregistrykey" data-raw-source="[&lt;strong&gt;RtlCheckRegistryKey&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlcheckregistrykey)"><strong>RtlCheckRegistryKey</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>1つ以上のレジストリキーの値を調べます。</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlqueryregistryvalues" data-raw-source="[&lt;strong&gt;RtlQueryRegistryValues&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlqueryregistryvalues)"><strong>RtlQueryRegistryValues</strong></a></p></td>
</tr>
<tr class="even">
<td><p>レジストリキー値を書き込む</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlwriteregistryvalue" data-raw-source="[&lt;strong&gt;RtlWriteRegistryValue&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlwriteregistryvalue)"><strong>RtlWriteRegistryValue</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>レジストリキーの値を削除します。</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtldeleteregistryvalue" data-raw-source="[&lt;strong&gt;RtlDeleteRegistryValue&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtldeleteregistryvalue)"><strong>RtlDeleteRegistryValue</strong></a></p></td>
</tr>
</tbody>
</table>

 

次のコード例では、 **\\Registry\\コンピューター\\システム\\** <em>KeyName</em>の値を 0xff*に設定する*方法を示します。 この例と、「[レジストリキーオブジェクトルーチン](registry-key-object-routines.md)」セクションの対応するものを比較します。

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

**Zw*xxx*キー**ルーチンの代わりに**Rtl*xxx*Registry * Xxx*** ルーチンを使用する場合は、記述するコードの数を減らすことができますが、後者は、特定の操作を実行するために必要です。 たとえば、 [**ZwEnumerateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratekey)に対応する**Rtl*xxx*Registry * Xxx*** ルーチンは存在しません。

同じキーに対して複数の操作を実行すると、 **Zw*Xxx*キー**ルーチンの方が効率的になります。各操作に対して同じ開いているハンドルを使用できます。 これに対し、 **Rtl*xxx*Registry * Xxx*** ルーチンは、各操作の新しいハンドルを開いて閉じます。

 

 




