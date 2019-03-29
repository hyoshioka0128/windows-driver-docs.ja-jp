---
title: オブジェクト
description: オブジェクトの拡張機能には、システムのオブジェクトに関する情報が表示されます。
ms.assetid: dc6d862b-3246-4d5b-992c-8723a0347f1d
keywords:
- Windows デバッグ オブジェクト
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- object
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3283e0d3d6c6bcec07896d8943ca1e9b19974808
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572900"
---
# <a name="object"></a>!object


**! オブジェクト**拡張機能がシステム オブジェクトに関する情報を表示します。

```dbgcmd
!object Address [Flags] 
!object Path
!object 0 Name 
!object -p
!object {-h|-?}
```

## <a name="span-idddkobjectdbgspanspan-idddkobjectdbgspanparameters"></a><span id="ddk__object_dbg"></span><span id="DDK__OBJECT_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
最初の引数が 0 以外の 16 進数である場合は、表示するシステム オブジェクトの 16 進数のアドレスを指定します。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
コマンドの出力の詳細レベルを指定します。

設定*フラグ*にこれらの値のビット演算 OR。

<span id="0x0"></span><span id="0X0"></span>**0x0**  
オブジェクトの種類を表示します。

<span id="0x1"></span><span id="0X1"></span>**0x1**  
表示オブジェクトの種類、オブジェクト名、および参照カウントします。

<span id="0x8"></span><span id="0X8"></span>**0x8**  
オブジェクト ディレクトリの内容またはシンボリック リンクのターゲットを表示します。 このフラグは場合のみ有効**0x1**も設定されます。

<span id="0x10"></span><span id="0X10"></span>**0x10**  
省略可能なオブジェクトのヘッダーを表示します。

<span id="0x20"></span><span id="0X20"></span>**0x20**  
名前付きのオブジェクトへの完全なパスを表示します。 このフラグは場合のみ有効**0x1**も設定されます。

*フラグ*パラメーターは省略可能です。 既定値は、0x9 です。

<span id="_______Path______"></span><span id="_______path______"></span><span id="_______PATH______"></span> *パス*   
最初の引数は、円記号で始まる場合 (\)、 **! オブジェクト**オブジェクトのパス名として解釈します。 このオプションを使用する場合は、オブジェクト マネージャーによって使用されるディレクトリ構造に従って、表示が配置されます。

<span id="_______Name______"></span><span id="_______name______"></span><span id="_______NAME______"></span> *名*   
最初の引数がゼロの場合、2 番目の引数は、すべてのインスタンスを表示する対象のシステム オブジェクトのクラスの名前として解釈されます。

<span id="_______-p"></span><span id="_______-P"></span> **-p**  
名前空間のプライベート オブジェクトを表示します。

<span id="-h-_"></span><span id="-H-_"></span>{**-h**|**-?**}  
このコマンドのヘルプを表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>例

この例では、パスの\\デバイス ディレクトリ **! オブジェクト**。 すべてのオブジェクトの一覧が、出力、\\デバイスのディレクトリ。

```dbgcmd
0: kd> !object \Device
Object: ffffc00b074166a0  Type: (ffffe0083b768690) Directory
    ObjectHeader: ffffc00b07416670 (new version)
    HandleCount: 0  PointerCount: 224
    Directory Object: ffffc00b074092e0  Name: Device

    Hash Address          Type          Name
    ---- -------          ----          ----
     00  ffffe0083e6a61f0 Device        00000044
         ffffe0083dcc4050 Device        00000030
         ffffe0083d34f050 Device        NDMP2
         ffffe0083bdf7060 Device        NTPNP_PCI0002
         ...
         ffffe0083b85d060 Device        USBPDO-8
         ffffe0083d33d050 Device        USBFDO-6
         ...
         ffffe0083bdf0060 Device        NTPNP_PCI0001
```

表示されているオブジェクトは、のいずれかを選択すると、USBPDO 8 があるとします。 USBPDO 8 (ffffe0083b85d060) のアドレスに渡す **! オブジェクト**t です。 設定*フラグ*最小限の情報を取得するには、「0x0」にします。

```dbgcmd
0: kd> !object ffffe0083b85d060 0x0
Object: ffffe0083b85d060  Type: (ffffe0083b87df20) Device
    ObjectHeader: ffffe0083b85d030 (new version)
```

設定して、同じオブジェクトの名前と参照カウントの情報を含める*フラグ*0x1 です。

```dbgcmd
0: kd> !object ffffe0083b85d060 0x1
Object: ffffe0083b85d060  Type: (ffffe0083b87df20) Device
    ObjectHeader: ffffe0083b85d030 (new version)
    HandleCount: 0  PointerCount: 6
    Directory Object: ffffc00b074166a0  Name: USBPDO-8
```

設定して、同じオブジェクトの省略可能なヘッダー情報を取得*フラグ*0x10 にします。

```dbgcmd
0: kd> !object ffffe0083b85d060 0x10
Object: ffffe0083b85d060  Type: (ffffe0083b87df20) Device
    ObjectHeader: ffffe0083b85d030 (new version)
Optional Headers: 
    NameInfo(ffffe0083b85d010)
```

次の例では **! オブジェクト**ディレクトリ オブジェクトの 2 回クリックします。 初めて 0x8 フラグが設定されていないため、ディレクトリの内容は表示されません。 2 回目、0x8 と 0x1 の両方のフラグが設定されているため、ディレクトリの内容が表示されます (フラグ = 0x9)。

```dbgcmd
0: kd> !object ffffc00b07481d00 0x1
Object: ffffc00b07481d00  Type: (ffffe0083b768690) Directory
    ObjectHeader: ffffc00b07481cd0 (new version)
    HandleCount: 0  PointerCount: 3
    Directory Object: ffffc00b07481eb0  Name: Filters

0: kd> !object ffffc00b07481d00 0x9
Object: ffffc00b07481d00  Type: (ffffe0083b768690) Directory
    ObjectHeader: ffffc00b07481cd0 (new version)
    HandleCount: 0  PointerCount: 3
    Directory Object: ffffc00b07481eb0  Name: Filters

    Hash Address          Type          Name
    ---- -------          ----          ----
     19  ffffe0083c5f56e0 Device        FltMgrMsg
     21  ffffe0083c5f5060 Device        FltMgr
```

次の例では **! オブジェクト**SymbolicLink オブジェクトに対して 2 回です。 初めて 0x8 フラグが設定されていないために、シンボリック リンクのターゲットは表示されません。 2 回目、0x8 と 0x1 の両方のフラグが設定されているために、シンボリック リンクのターゲットを splayed は (フラグ = 0x9)。

```dbgcmd
0: kd> !object ffffc00b07628fb0 0x1
Object: ffffc00b07628fb0  Type: (ffffe0083b769450) SymbolicLink
    ObjectHeader: ffffc00b07628f80 (new version)
    HandleCount: 0  PointerCount: 1
    Directory Object: ffffc00b074166a0  Name: Ip6

0: kd> !object ffffc00b07628fb0 0x9
Object: ffffc00b07628fb0  Type: (ffffe0083b769450) SymbolicLink
    ObjectHeader: ffffc00b07628f80 (new version)
    HandleCount: 0  PointerCount: 1
    Directory Object: ffffc00b074166a0  Name: Ip6
    Target String is '\Device\Tdx'
```

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

オブジェクトとオブジェクト マネージャーについては、Microsoft Windows SDK ドキュメントに、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[オブジェクト参照のトレース](object-reference-tracing.md)

[**!obtrace**](-obtrace.md)

[**!handle**](-handle.md)

[オブジェクトの ACL の決定](determining-the-acl-of-an-object.md)

[カーネル モード拡張コマンド](kernel-mode-extensions.md)

 

 






