---
title: PC カード構成が不完全とアドレスを登録します。
description: 構成が不完全レジスタのアドレスを持つ PC カードをサポートする方法について
ms.assetid: 2a708ca5-a119-4ef5-81ee-d9e40e7a5255
keywords:
- 不完全な構成は、WDK の多機能デバイスを登録します。
- システム提供の多機能バス ドライバー WDK
- mf.sys
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27326a54cb459dbee9eccbd81dcd5bf0e8d04465
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386379"
---
# <a name="pc-cards-with-incomplete-configuration-register-addresses"></a>PC カード構成が不完全とアドレスを登録します。


多機能 16 ビット PC カード デバイスが各関数のレジスタを構成するすべての属性のメモリ内のポインターが含まれていない場合は、セットを登録 (、LONGLINK をサポートしていません\_MFC タプル)、このようなデバイスのベンダーを使用して、システム提供の多機能は現在バス ドライバー (mf.sys) が、カスタム INF ファイルを提供、および個々 の関数をサポートする必要があります。

NT ベースのプラットフォーム上のようなデバイスの製造元は、多機能デバイスは、システムによって提供される関数のドライバーを使用できます。

デバイスのカスタム INF では、デバイスの機能のドライバーとして mf.sys を指定する必要があります。 システム提供の mf.sys ドライバーにし、デバイスの機能が列挙されます。

参照してください[System-Supplied 多機能バス ドライバーを使用して](using-the-system-supplied-multifunction-bus-driver.md)詳細については、システム提供の mf.sys ドライバーを使用します。

このようなデバイスの製造元は、次で提供する必要があります。

-   多機能デバイスのカスタム INF ファイルです。 (ベンダーから提供された)

    仕入先には、多機能バス ドライバーとして mf.sys を指定します、(とその関連付けられている GUID として devguid.h で定義されている)、「多機能」クラスを指定し、不足している構成の登録アドレスを提供する多機能 INF ファイルを指定する必要があります。 さらに、このセクションで後述する情報も参照してください。

-   デバイスの各関数の関数の PnP ドライバー。 (ベンダーから提供された)

    多機能バス ドライバーでは、多機能のセマンティクスを処理するため、関数ドライバーは、関数が個々 のデバイスとしてパッケージ化するときに使用される同じドライバーを指定できます。

-   各関数の場合、デバイスの INF ファイル。 (ベンダーから提供された)

    INF ファイルには、関数が個々 のデバイスとしてパッケージ化するときに使用される同じファイルを指定できます。 INF ファイルでは、多機能の特殊なセマンティクスは必要ありません。

多機能デバイスのようなカスタムの INF には、少なくとも 1 つ含める必要があります[ **INF DDInstall.LogConfigOverride セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-logconfigoverride-section)します。 Override セクションを含める必要があります、 **MfCardConfig**レジスタの各セットの場所の特定の各関数のエントリ。

INF では、上書きの構成、INF に存在する場合は、PnP マネージャーは、デバイスから、デバイスのリソース要件を使用しないために、デバイスで指定されたすべてのリソース要件を再確認する必要があります。

指定、 **MfCardConfig**で説明する構文を使用してエントリ[ **INF LogConfig ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-logconfig-directive)します。

たとえば、多機能 PC カード デバイスのモデムとネットワーク アダプターを含むカスタム INF から次の抜粋を考えてみます。

```cpp
;...
 
[DDInstall.LogConfigOverride]
LogConfig = DDInstall.Override0
 
[DDInstall.Override0]
IOConfig     =    3F8-3FF                  ; Com1
IOConfig     =    10@100-FFFF%FFF0         ; NIC I/O
IRQConfig    =    3,4,5,7,9,10,11          ; IRQ
MemConfig    =    2000@0-FFFFFFFF%FFFFE000 ; Memory Descriptor 0
MemConfig    =    1000@0-FFFFFFFF%FFFFF000 ; Memory Descriptor 1
MfCardConfig =    1000:47:0(A)
MfCardConfig =    1080:47:1
;...
```

2 つの例を示します**MfCardConfig**エントリ、デバイスの各関数の 1 つ。 最初の**MfCardConfig**エントリには、次の情報が含まれています。

<a href="" id="1000--configregbase-"></a>1000 (*ConfigRegBase*)  
オフセット 0x1000 カードの属性のメモリ内の構成のレジスタのセットがあることを指定します。 この例では、これらのレジスタの情報は、カードのモデム関数について説明します。

<a href="" id="47--configoptions-"></a>47 (*ConfigOptions*)  
構成オプションのレジスタにバス ドライバーのプログラムを 16 進数の値を指定します、 *ConfigRegBase*オフセット (0x1000)。

<a href="" id="0--ioconfigindex-"></a>0 (*IoConfigIndex*)  
この関数の I/O リソースが最初に表示されていることを指定します。 **IOConfig**このセクションのエントリ。 インデックスはゼロがあり、この例では最初のエントリを示す"**IOConfig** 3f8-3ff ="。

<a href="" id="a--attrs-"></a>A (*属性*)  
この関数は、通常、モデムのオーディオの有効化を有効にするバス ドライバーに指示します。

2 番目の**MfCardConfig**エントリには、デバイス (この例はネットワーク アダプター) の 2 番目の関数に関する情報が含まれています。 このエントリは、2 つ目のオフセット 0x1080 レジスタのセットがあることを指定します。 バス ドライバーの記述、 *ConfigOptions* 0x47 をこの関数の構成オプションのレジスタの値。 *IoConfigIndex*いずれかの値を使用して、2 つ目のバス ドライバーに指示**IOConfig**このセクションのエントリ (**IOConfig** = 10@100-FFFF%fff0) I/O ベースのプログラミングこの関数のレジスタを制限してください。

1 つ以上含める*DDInstall*. **オーバーライド * * * N*非順次 I/O ポートの範囲の 1 つ以上の選択肢を指定する INF セクション。

デバイスが 0 に基づいていない場合は、[メモリ] ウィンドウを使用している場合、 *DDInstall*. **オーバーライド * * * N*セクションに含める必要がありますも、 **PcCardConfig**エントリ。 Override セクションでは、両方を持つ場合、 **MfCardConfig**エントリと**PcCardConfig**エントリ、PCMCIA バス ドライバーの無視、 *ConfigIndex*値、 **PcCardConfig**だけ使用してエントリ、 *MemoryCardBaseN*情報。 参照してください[をサポートしている PC カードことがある不完全な構成を登録](supporting-pc-cards-that-have-incomplete-configuration-registers.md)の詳細については、 **PcCardConfig**エントリ。

 

 




