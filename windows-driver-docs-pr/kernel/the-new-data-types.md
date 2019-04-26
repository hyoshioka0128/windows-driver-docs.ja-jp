---
title: 新しいデータ型
description: 新しいデータ型
ms.assetid: 13a0d51e-0a9a-471f-8427-d4a7a7eb6459
keywords:
- 64 ビットの WDK カーネル、ドライバーの移植
- 64 ビット Windows に移植ドライバー
- データ型の WDK 64 ビット
- WDK の 64 ビットの固定精度の整数型します。
- WDK の 64 ビットのポインターの精度の整数型します。
- 特定の有効桁数のポインター型の WDK 64 ビット
- データ型の変換
- 64 ビット WDK カーネルでは、データ型
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85c1158f8a67c31d017f5aaf15d0db117825f776
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353560"
---
# <a name="the-new-data-types"></a>新しいデータ型





新しいデータ型の 3 つのクラスがあります。 固定有効桁数の整数型、ポインターの精度の整数型、および有効桁数の特定のポインター型。 これらの型は、開発者が登場する前にも 64 ビット Windows の準備 (具体的には、Basetsd.h) を Windows 環境に追加されました。 これらの新しい型はされた既存のコードで作業できるように、C 言語の基本整数型および long の型から派生します。 そのため、これらのデータ、コード内の型、32 ビットの Windows 上のコードをテストし 64 ビット コンパイラを使用して検索し、事前に移植性の問題を修正、ためには、ドライバーが準備を完了すると、64 ビット Windows できますでテストできるを使用します。

さらに、これらの新しいデータ型を採用すると、コードより堅牢ななります。 これらのデータ型を使用するには、安全でないポインターの使用方法、ポリモーフィズム、およびデータ定義用のコードをスキャンする必要があります。 安全のためには、新しい型を使用します。 たとえば、された変数型の**ULONG\_PTR**、算術演算またはポリモーフィズムのキャストのポインターに対して使用されることは明らかです。 ネイティブの Win32 データ型を使用して直接このような使用状況を示すことはできません。 派生型の名前付けまたはハンガリアン記法を使用して、これを行うことができますが、両方の手法が発生したエラーを起こしやすい。

### <a name="fixed-precision-integer-types"></a>固定精度の整数型

固定精度のデータ型は、32 ビットおよび 64 ビット プログラミングの長さは同じです。 これを思い出すのに役立つには、その有効桁数は、データ型の名前の一部です。 固定精度のデータ型を次に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>種類</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DWORD32</strong></p></td>
<td><p>32 ビット符号なし整数</p></td>
</tr>
<tr class="even">
<td><p><strong>DWORD64</strong></p></td>
<td><p>64 ビット符号なし整数</p></td>
</tr>
<tr class="odd">
<td><p><strong>INT32</strong></p></td>
<td><p>32 ビット符号付き整数</p></td>
</tr>
<tr class="even">
<td><p><strong>INT64</strong></p></td>
<td><p>64 ビット符号付き整数</p></td>
</tr>
<tr class="odd">
<td><p><strong>LONG32</strong></p></td>
<td><p>32 ビット符号付き整数</p></td>
</tr>
<tr class="even">
<td><p><strong>LONG64</strong></p></td>
<td><p>64 ビット符号付き整数</p></td>
</tr>
<tr class="odd">
<td><p><strong>UINT32</strong></p></td>
<td><p>符号なし<strong>INT32</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>UINT64</strong></p></td>
<td><p>符号なし<strong>INT64</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>ULONG32</strong></p></td>
<td><p>Unsigned <strong>LONG32</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>ULONG64</strong></p></td>
<td><p>Unsigned <strong>LONG64</strong></p></td>
</tr>
</tbody>
</table>

 

### <a name="pointer-precision-integer-types"></a>ポインターの精度の整数型

(64 ビット プラットフォーム用にコンパイルされるときに 64 ビット、32 ビット プラットフォーム用にコンパイルされるときに、32 ビットになります)、つまり、ポインターの精度の変化に応じてこれらのデータ型がそれに応じて有効桁数を反映します。 したがって、ポインターの算術演算を実行するときに、これらの型のいずれかへのポインターをキャストしても安全です。ポインターの精度が 64 ビットの場合は、型は、64 ビットです。 カウントの種類では、最大サイズのポインターが参照することができますも反映されます。 ポインターの精度とカウントの種類を次に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>種類</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DWORD_PTR</strong></p></td>
<td><p>ポインターの精度の符号なし long 型。</p></td>
</tr>
<tr class="even">
<td><p><strong>HALF_PTR</strong></p></td>
<td><p>符号付きの半分ポインターの精度 (32 ビット システムでは、64 ビット システムで 32 ビットの 16 ビット) の整数の型。</p></td>
</tr>
<tr class="odd">
<td><p><strong>INT_PTR</strong></p></td>
<td><p>符号付きポインターの精度の整数の型。</p></td>
</tr>
<tr class="even">
<td><p><strong>LONG_PTR</strong></p></td>
<td><p>Long 型のポインターの精度を署名します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SIZE_T</strong></p></td>
<td><p>バイトのポインターは参照先の最大数。 ポインターの完全な範囲にまたがる必要がある数のこの型を使用します。</p></td>
</tr>
<tr class="even">
<td><p><strong>SSIZE_T</strong></p></td>
<td><p>署名<strong>SIZE_T</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UHALF_PTR</strong></p></td>
<td><p>符号なし<strong>HALF_PTR</strong>します。</p></td>
</tr>
<tr class="even">
<td><p><strong>UINT_PTR</strong></p></td>
<td><p>符号なし<strong>INT_PTR</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ULONG_PTR</strong></p></td>
<td><p>符号なし<strong>LONG_PTR</strong>します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="fixed-precision-pointer-types"></a>固定精度のポインター型

ポインターのサイズを明示的に新しいポインター型もあります。 64 ビット コードでこれらのポインター型を使用する場合は注意してください。32 ビットのタイプを使用してポインターを宣言する場合は、64 ビット ポインターを切り捨てることによって、ポインターが作成されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>種類</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>POINTER_32</strong></p></td>
<td><p>32 ビットのポインター。 32 ビット システムでは、これはネイティブ ポインターです。 64 ビット システムでは、これは切り捨てられた 64 ビットのポインターです。</p></td>
</tr>
<tr class="even">
<td><p><strong>POINTER_64</strong></p></td>
<td><p>64 ビットのポインター。 64 ビット システムでは、これはネイティブ ポインターです。 32 ビット システムでは、これは 32 ビットの符号拡張ポインターです。</p>
<p>高ポインター ビットの状態を想定する安全ではないことに注意してください。</p></td>
</tr>
</tbody>
</table>

 

### <a name="helper-functions"></a>ヘルパー関数

(Basetsd.h で定義された) 次のインライン関数役立つ安全に変換値 1 つの型から別に示します。

```cpp
unsigned long HandleToUlong( const void *h )
long HandleToLong( const void *h )
void * LongToHandle( const long h )
unsigned long PtrToUlong( const void *p )
unsigned int PtrToUint( const void *p )
unsigned short PtrToUshort( const void *p )
long PtrToLong( const void *p )
int PtrToInt( const void *p )
short PtrToShort( const void *p )
void * IntToPtr( const int i )
void * UIntToPtr( const unsigned int ui )
void * LongToPtr( const long l )
void * ULongToPtr( const unsigned long ul )
```

**警告**  **IntToPtr**符号拡張、 **int**値、 **UIntToPtr**ゼロ拡張、符号なし**int**値、 **LongToPtr**符号拡張、**長い**値、および**ULongToPtr**ゼロ拡張、 **unsigned long**値。

 

 

 




