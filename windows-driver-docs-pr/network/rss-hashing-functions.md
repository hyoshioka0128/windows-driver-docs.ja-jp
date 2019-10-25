---
title: RSS ハッシュ関数
description: RSS ハッシュ関数
ms.assetid: e7698573-c3d1-4ac6-a985-93cf7fc6e585
keywords:
- 受信側のスケーリング WDK ネットワーク、ハッシュ
- RSS WDK ネットワーク、ハッシュ
- ハッシュ WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7603cb30b39da21b605d1be6bd5d1cb8a3fa584
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842006"
---
# <a name="rss-hashing-functions"></a>RSS ハッシュ関数


## <a name="overview"></a>概要

NIC またはそのミニポートドライバーは、rss ハッシュ値を計算するために RSS ハッシュ関数を使用します。

それ以降のドライバーは、ハッシュの種類、関数、およびテーブルを設定して、Cpu への接続を割り当てます。 詳細については、「 [RSS の構成](rss-configuration.md)」を参照してください。

ハッシュ関数は、次のいずれかになります。

- **NdisHashFunctionToeplitz**
- **NdisHashFunctionReserved1**
- **NdisHashFunctionReserved2**
- **NdisHashFunctionReserved3**

>[!NOTE]
> 現時点では、ミニポートドライバーで使用できる唯一のハッシュ関数は**NdisHashFunctionToeplitz**です。 その他のハッシュ関数は、NDIS 用に予約されています。 

ミニポートドライバーは、ドライバーが受信データを示す前に、各[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造体で使用されるハッシュ関数と値を識別する必要があります。 詳細については、「 [RSS 受信データの表示](indicating-rss-receive-data.md)」を参照してください。

## <a name="examples"></a>例

次の4つの擬似コード例は、 **NdisHashFunctionToeplitz**ハッシュ値を計算する方法を示しています。 これらの例は、 **NdisHashFunctionToeplitz**で使用可能な4つのハッシュの種類を表しています。 ハッシュの種類の詳細については、「 [RSS ハッシュの種類](rss-hashing-types.md)」を参照してください。

この例を簡単にするために、入力バイトストリームを処理する一般化されたアルゴリズムが必要です。 バイトストリームの特定の形式は、後の4つの例で定義されています。

このドライバーは、ハッシュ計算で使用するシークレットキー (K) をミニポートドライバーに提供します。 キーの長さは40バイト (320 ビット) です。 キーの詳細については、「 [RSS の構成](rss-configuration.md)」を参照してください。

*N*バイトを含む入力配列を指定すると、バイトストリームは次のように定義されます。

```c++
input[0] input[1] input[2] ... input[n-1]
```

左端のバイトは\[0\]になり、入力\[0\] の最上位ビットが左端になります。 右端のバイトは\[n-1\]の入力であり、最小ビットの入力\[n-1\] が右端になりますが、です。

上記の定義により、一般的な入力バイトストリームを処理するための擬似コードは次のように定義されます。

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

擬似コードには @n-mの形式のエントリが含まれています。 これらのエントリは、TCP パケット内の各要素のバイト範囲を識別します。

### <a name="example-hash-calculation-for-ipv4-with-the-tcp-header"></a>TCP ヘッダーを使用した IPv4 のハッシュ計算の例

パケット内で発生した順序を維持したまま、パケットの SourceAddress、DestinationAddress、Sourceaddress、および Destinationaddress の各フィールドをバイト配列に連結します。

```c++
Input[12] = @12-15, @16-19, @20-21, @22-23
Result = ComputeHash(Input, 12)
```

### <a name="example-hash-calculation-for-ipv4-only"></a>IPv4 のみのハッシュ計算の例

パケットの SourceAddress フィールドと DestinationAddress フィールドを連結して、バイト配列にします。

```c++
Input[8] = @12-15, @16-19
Result = ComputeHash(Input, 8) 
```

### <a name="example-hash-calculation-for-ipv6-with-the-tcp-header"></a>TCP ヘッダーを使用した IPv6 のハッシュ計算の例

パケット内で発生した順序を維持したまま、パケットの SourceAddress、DestinationAddress、Sourceaddress、および Destinationaddress の各フィールドをバイト配列に連結します。

```c++
Input[36] = @8-23, @24-39, @40-41, @42-43
Result = ComputeHash(Input, 36)
```

### <a name="example-hash-calculation-for-ipv6-only"></a>IPv6 のみのハッシュ計算の例

パケットの SourceAddress フィールドと DestinationAddress フィールドを連結して、バイト配列にします。

```c++
Input[32] = @8-23, @24-39
Result = ComputeHash(Input, 32)
```

 

 





