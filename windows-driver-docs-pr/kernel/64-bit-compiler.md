---
title: 64 ビット コンパイラ
description: 64 ビット コンパイラ
ms.assetid: c119d6b3-03e2-4ffc-b0a9-8077b141a2f1
keywords:
- 64 ビットの WDK カーネル、ドライバーの移植
- 64 ビット Windows に移植ドライバー
- WDK の 64 ビットのコンパイラ
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ddf89ab2851c8681f91e88c8a57c61ff4e23aa9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339211"
---
# <a name="64-bit-compiler"></a>64 ビット コンパイラ





使用する、32 ビット ドライバーのソース コードを変換した後、[新しいデータ型](the-new-data-types.md)、最初に不足している任意の種類に関連する問題を識別するために、64 ビット コンパイラを使用することができます。 初めての 64 ビット Windows では、このコードをコンパイルするコンパイラはポインター切り捨てまたは型の不一致の警告の数が多くを生成する可能性があります。 堅牢なコードにするためのガイドとしてこれらの警告を使用します。 ポインター切り捨ての警告では特に、すべての警告を排除することをお勧めします。

このような警告の例を次に示します。

```cpp
warning C4311: 'type cast' : pointer truncation from 'unsigned char *' to 'unsigned long '
```

たとえば、次のコードでは、警告 C4311 を生成できます。

```cpp
buffer = (PUCHAR)srbControl;
(ULONG)buffer += srbControl->HeaderLength;
```

コードを修正するには、次の変更を加えます。

```cpp
buffer = (PUCHAR)srbControl;
(ULONG_PTR)buffer += srbControl->HeaderLength;
```

### <a name="predefined-macros"></a>定義済みマクロ

コンパイラは、プラットフォームを識別するために次のマクロを定義します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>マクロ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>_WIN64</p></td>
<td><p>64 ビットのプラットフォームです。</p></td>
</tr>
<tr class="even">
<td><p>_WIN32</p></td>
<td><p>32 ビットのプラットフォームです。 この値は、旧バージョンとの互換性のため、64 ビット コンパイラによっても定義されます。</p></td>
</tr>
<tr class="odd">
<td><p>_WIN16</p></td>
<td><p>16 ビットのプラットフォームです。</p></td>
</tr>
</tbody>
</table>

 

次のマクロは、アーキテクチャに固有です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>マクロ</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>_M_IA64</p></td>
<td><p>64 ビットの Intel プラットフォームです。</p></td>
</tr>
<tr class="even">
<td><p>_M_IX86</p></td>
<td><p>32 ビットの Intel プラットフォームです。</p></td>
</tr>
</tbody>
</table>

 

アーキテクチャ固有のコードでは、を除き、これらのマクロを使用しないでください。 代わりに、 \_WIN64、 \_WIN32、および\_WIN16 可能な場合。

### <a name="64-bit-compiler-switches-and-warnings"></a>64 ビットのコンパイラ スイッチと警告

64 ビット Windows への移植を支援するために、警告のオプションがあります。 -Wp64-W3 スイッチにより、次の警告。

-   **C4305**:切り捨ての警告。 たとえば、"return": 切り捨てに"符号なしの int64"から"long"。

-   **C4311**:切り捨ての警告。 たとえば、「キャストを入力」: からポインター切り捨て"int\*\_ptr64""int"へ

-   **C4312**:大きなサイズの警告への変換。 たとえば、「キャストを入力」: 変換するには、"int"から"int\*\_ptr64"より大きいサイズの。

-   **C4318**:長さが 0 を渡します。 たとえば、長さとして定数ゼロを渡すこと、 **memset**関数。

-   **C4319**:Not 演算子。 たとえば、"~": ゼロ拡張"unsigned long"に"符号なし\_int64"より大きいサイズの。

-   **C4313**:呼び出す、 **printf**ファミリの関数が競合する変換指定子と引数を入力します。 たとえば、"printf":"%p"書式指定文字列では、型の引数 2 と競合"\_int64"。 別の例は、printf 関数の呼び出し ("%x"、ポインター\_値)。 これにより、切り捨ての上位 32 ビット。 適切な呼び出しは、printf ("%p"、ポインター\_値)。

-   **C4244**:既存の警告 C4242 と同じです。 たとえば、"return": からの変換"\_int64"データ損失の可能性"unsigned int"にします。

 

 




