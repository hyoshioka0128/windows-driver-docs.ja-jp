---
title: プリンター メモリ構成の説明
description: プリンター メモリ構成の説明
ms.assetid: 4a85788a-9713-42fb-a788-4d45f9aaabac
keywords:
- Unidrv、プリンター メモリの構成
- GPD ファイル WDK Unidrv、プリンター メモリの構成
- プリンター メモリ構成 WDK Unidrv
- WDK Unidrv 用メモリ構成
- Unidrv WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ce5a5c887787cbdc0ae2ee997e135170e91bb36
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355674"
---
# <a name="describing-printer-memory-configurations"></a>プリンター メモリ構成の説明





Unidrv がプリンターのメモリ使用量の追跡を試みることができるように、Unidrv ミニドライバーは、プリンターの可能な限り、既定のメモリ構成の説明を含めることができます。 各メモリ構成の説明には、メモリの合計および使用可能なメモリの両方の値が含まれています。 ページ、および Unidrv によって制御されるその他の操作を保護するフォントをダウンロードするのには、使用可能なメモリを使用できます。

GPD ファイル内では、プリンターの考えられるメモリの構成を記述するのに 2 つのメソッドを使用できます。 両方の方法では、内の属性を指定する必要があります、\*機能の 1 つであるメモリ機能のエントリの[標準機能](standard-features.md)します。 2 つの方法は次のとおりです。

1.  すべての可能な構成を指定するには個別の\*オプション内のエントリ、\*機能のエントリ。 各\*オプションのエントリを含める必要があります、 \*MemoryConfigKB 属性に説明されている、[メモリ機能のオプション属性](option-attributes-for-the-memory-feature.md)します。

    たとえば、プリンターが 2 つのメモリ構成、450 キロバイトの使用可能な 1 メガバイトの構成および使用可能な 1350 キロバイト 2 メガバイトの構成に使用できることを指定するには、GPD の次のエントリを使用できます。

    ```cpp
    *Feature: Memory
    {
        *Name: "Printer Memory"
        *DefaultOption: 1MB
        *Option: 1MB
        {
            *Name: "Standard 1MB"
            *MemoryConfigKB: PAIR(1024, 450)
        }
        *Option: 2MB 
        {
            *Name: "Add-On 2MB"
            *MemoryConfigKB: PAIR(2048,1350)
        }
    }
     
    ```

2.  または、\*機能のエントリは、1 つまたは複数含めることができます\*MemConfigKB または\*MemConfigMB の属性の代わりに\*エントリのオプションします。 これは、単に含めず、一連のメモリ オプションを指定する方法\*エントリのオプションします。 各\*MemConfigKB または\*MemConfigMB 属性は、メモリのオプションを表します。

    たとえば、同じ 2 つの構成、使用可能な 450 キロバイトで 1 メガバイト構成および 2 メガバイト構成で使用可能な 1350 キロバイトを指定する、次の GPD エントリを使用できます。

    ```cpp
    *Feature: Memory
    {
        *Name: "Printer Memory"
        *DefaultOption: 1024KB
        *MemConfigKB: PAIR(1024, 450)
        *MemConfigKB: PAIR(2048, 1350)
    }
     
    ```

    GPD パーサーは、ペアのステートメントの最初のエントリに基づいて、各構成の表示可能なオプション名を作成します。 オプション名の例では、"1024 KB"と"2048 KB"になります。 引数、 \*DefaultOption 属性で、これらの名前と一致する必要があります。

内の 1 つ方法 1 と方法 2 の両方を使用できる\*機能のエントリ。

オプションのパーサーによって生成された名前は、ローカライズの要件と互換性がない、方法 1 を使用して、メソッドが 2 ではなく。

どちらの方法を使用する、 [Unidrv ユーザー インターフェイス](unidrv-user-interface.md)デバイスのプリンターのプロパティ シートでメモリの機能オプションが表示されます。

ミニドライバーは、メモリの構成を指定する場合は、プリンターのメモリに格納できるし、使用可能な領域を使用してデータの種類も指定できます。 \*MemoryUsage 属性は、のいずれか、[プリンター機能属性](printer-capability-attributes.md)フォント、ラスター、またはベクター データ、または、3 つの組み合わせはプリンターのメモリ内に格納されているかどうかを Unidrv に示すために使用するとします。 各型を指定すると、Unidrv は使用されて、プリンター メモリの量を追跡しようとします。

 

 




