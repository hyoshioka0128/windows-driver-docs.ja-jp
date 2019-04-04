---
title: RSS ハッシュ関数
description: RSS ハッシュ関数
ms.assetid: e7698573-c3d1-4ac6-a985-93cf7fc6e585
keywords:
- 受信側スケーリング WDK ネットワーク、ハッシュ
- RSS の WDK にネットワーク接続、ハッシュ
- WDK RSS ハッシュ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3559780bdce1a6a0896cd6e599afac6c4a22d121
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527258"
---
# <a name="rss-hashing-functions"></a>RSS ハッシュ関数


## <a name="overview"></a>概要

NIC のミニポート ドライバー、RSS ハッシュ関数でを使用して RSS ハッシュ値を計算します。

ドライバーの重なって Cpu への接続を割り当てるには、ハッシュ型、関数、およびテーブルを設定します。 詳細については、[RSS 構成](rss-configuration.md)を参照してください。

ハッシュ関数には、次のいずれかを指定できます。

- **NdisHashFunctionToeplitz**
- **NdisHashFunctionReserved1**
- **NdisHashFunctionReserved2**
- **NdisHashFunctionReserved3**

>[!NOTE]
> 現時点では、 **NdisHashFunctionToeplitz**は唯一のハッシュ関数をミニポート ドライバーを使用できます。 他のハッシュ関数は、NDIS 用に予約されています。 

ミニポート ドライバーは、ハッシュ関数と各で使用される値を識別する必要があります[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)受信したデータの構造体の前に、ドライバーを示します。 詳細については、[RSS の受信データのことを示す](indicating-rss-receive-data.md)を参照してください。

## <a name="examples"></a>例

次の 4 つの擬似コード例を計算する方法を示して、 **NdisHashFunctionToeplitz**ハッシュ値。 これらの例は、利用できる 4 つの可能なハッシュ型を表す**NdisHashFunctionToeplitz**します。 ハッシュの種類の詳細については、[RSS ハッシュ型](rss-hashing-types.md)を参照してください。

例を簡素化するには、入力バイト ストリームを処理する汎用的なアルゴリズムが必要です。 バイト ストリームの特定の形式は、4 つの例では後で定義されます。

上位のドライバーは、ハッシュ計算で使用するため、ミニポート ドライバーに秘密キー (K) を提供します。 長さ 40 バイト (320 bits) が重要です。 キーの詳細については、[RSS 構成](rss-configuration.md)を参照してください。

入力を含む配列を指定した*n*バイト、バイト ストリームは次のように定義されています。

```c++
input[0] input[1] input[2] ... input[n-1]
```

左端のバイトの入力\[0\]、および入力の最上位ビット\[0\]一番左のビットです。 右端のバイトの入力\[n-1\]、および入力の最下位ビット\[n-1\]右端のビットです。

前述の定義を指定するには、一般的な入力バイト ストリームを処理するための疑似コードは次のように定義されます。

```c++
ComputeHash(input[], n)

result = 0
For each bit b in input[] from left to right
{
if (b == 1) result ^= (left-most 32 bits of K)
shift K left 1 bit position
}

return result
```

擬似コードには、フォームのエントリが含まれています。@n-mします。 これらのエントリは、TCP パケット内の各要素のバイト範囲を特定します。

### <a name="example-hash-calculation-for-ipv4-with-the-tcp-header"></a>Ipv4 の場合、TCP ヘッダーでハッシュ計算の例

パケットで発生した順序を維持し、バイト配列に、パケットの発信元アドレス、DestinationAddress、SourcePort、および DestinationPort フィールドを連結します。

```c++
Input[12] = @12-15, @16-19, @20-21, @22-23
Result = ComputeHash(Input, 12)
```

### <a name="example-hash-calculation-for-ipv4-only"></a>IPv4 のみのハッシュ計算の例

バイト配列には、パケットの発信元アドレスと DestinationAddress フィールドを連結します。

```c++
Input[8] = @12-15, @16-19
Result = ComputeHash(Input, 8) 
```

### <a name="example-hash-calculation-for-ipv6-with-the-tcp-header"></a>TCP ヘッダーと IPv6 のハッシュ計算の例

パケットに発生した順序を維持し、バイト配列には、パケットの発信元アドレス、DestinationAddress、SourcePort、および DestinationPort フィールドを連結します。

```c++
Input[36] = @8-23, @24-39, @40-41, @42-43
Result = ComputeHash(Input, 36)
```

### <a name="example-hash-calculation-for-ipv6-only"></a>IPv6 のみのハッシュ計算の例

バイト配列には、パケットの発信元アドレスと DestinationAddress フィールドを連結します。

```c++
Input[32] = @8-23, @24-39
Result = ComputeHash(Input, 32)
```

 

 





