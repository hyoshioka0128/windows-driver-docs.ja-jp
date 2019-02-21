---
title: for_each_function
description: For_each_function 拡張機能では、名前を持つ指定したパターンに一致する指定されたモジュールでの各関数のデバッガー コマンドを実行します。
ms.assetid: D51C3562-3D49-4528-A208-71A8756EBC8E
keywords:
- Windows デバッグ for_each_function
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- for_each_function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d9699254771ad1784fd6009d97c46639f41ad429
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529804"
---
# <a name="foreachfunction"></a>! の\_各\_関数


**! の\_各\_関数**拡張機能は、名前を持つ指定したパターンに一致する指定されたモジュールでの各関数のデバッガー コマンドを実行します。

```dbgcmd
!for_each_function -m:ModuleName -p:Pattern -c:CommandString
!for_each_function -?
```

## <a name="span-idddkvaddbgspanspan-idddkvaddbgspanparameters"></a><span id="ddk__vad_dbg"></span><span id="DDK__VAD_DBG"></span>パラメーター


<span id="_______-m_ModuleName______"></span><span id="_______-m_modulename______"></span><span id="_______-M_MODULENAME______"></span> -m:*ModuleName*   
モジュール名を指定します。 この名前は、通常、ファイル名拡張子を除いたファイル名です。 場合によっては、モジュール名はファイル名から大幅に異なります。

<span id="-p_Pattern______"></span><span id="-p_pattern______"></span><span id="-P_PATTERN______"></span>-p:*パターン*   
照合するパターンを指定します。

<span id="_______-c_CommandString______"></span><span id="_______-c_commandstring______"></span><span id="_______-C_COMMANDSTRING______"></span> -c:*クラスヒント*   
パターンに一致する指定したモジュール、関数ごとに実行するデバッガー コマンドを指定します。

次のエイリアスを使用する*クラスヒント*します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Alias</th>
<th align="left">データの種類</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>@#SymbolName</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>シンボルの名前。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@#SymbolAddress</p></td>
<td align="left"><p>ULONG64</p></td>
<td align="left"><p>シンボルのアドレス。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>@#ModName</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>モジュール名。</p></td>
</tr>
<tr class="even">
<td align="left"><p>@# FunctionName</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>関数名。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______-_______"></span> -?   
この拡張機能のヘルプを表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ext.dll

<a name="remarks"></a>注釈
-------

次の例は、すべての関数名、PCI モジュール パターンに一致するを一覧表示する方法を示しています。\*読み取り\*します。

```dbgcmd
1: kd> !for_each_function -m:pci -p:*read* -c:.echo @#FunctionName

PciReadDeviceConfig
PciReadDeviceSpace
PciReadSlotIdData
PciExternalReadDeviceConfig
PiRegStateReadStackCreationSettingsFromKey
VmProxyReadDevicePathsFromRegistry
PpRegStateReadCreateClassCreationSettings
ExpressRootPortReadConfigSpace
PciReadRomImage
PciDevice_ReadConfig
PciReadDeviceConfigEx
PciReadSlotConfig
```

エイリアスがない前後に空白場合、は、内部のエイリアスを配置する必要があります、 [ **${}エイリアス インタープリター** ](-------alias-interpreter-.md)トークンです。

次の例は、関数名のパターンに一致のすべてのモジュール内のすべてのシンボルを一覧表示する方法を示しています。 \*CreateFile\*します。 @ エイリアス\#ModuleName の空白スペースによって前がありません。 内でそのため、配置、 [ **${}エイリアス インタープリター** ](-------alias-interpreter-.md)トークンです。

**注**  と混同しないでください、@\#ModuleName エイリアスを @\#モジュール名のエイリアスです。 @\#ModuleName はエイリアスに属している、 [ **! の\_各\_モジュール**](-for-each-module.md)拡張機能、および @\#モジュール名がエイリアスに属している、 **!\_各\_関数**拡張機能。

 

```dbgcmd
1: kd> !for_each_module !for_each_function -m:${@#ModuleName} -p:*CreateFile* -c:.echo @#SymbolName
nt!BiCreateFileDeviceElement
nt!NtCreateFile
...
Wdf01000!FxFileObject::_CreateFileObject
fltmgr!FltCreateFileEx2$fin$0
fltmgr!FltCreateFileEx2
...
Ntfs!TxfIoCreateFile
Ntfs!NtfsCreateFileLock
...
MpFilter!MpTxfpCreateFileEntryUnsafe
mrxsmb10!MRxSmbFinishLongNameCreateFile
...
srv!SrvIoCreateFile
```

コマンド ファイルを一連のコマンドを配置して使用することができます[  **$$ &gt; &lt; (スクリプト ファイルを実行)** ](-----------------------a---run-script-file-.md)と一致する各関数でこれらのコマンドを実行する、パターン。 Commands.txt という名前のファイルに次のコマンドが含まれているとします。

```dbgcmd
.echo
.echo @#FunctionName
u @#SymbolAddress L1
```

次の例では、Commands.text ファイル内のコマンドを実行して、モジュールでは、PCI、パターンに一致する各関数の\*読み取り\*します。

```dbgcmd
1: kd> !for_each_function -m:pci -p:*read* -c:$$><Commands.txt

PciReadDeviceConfig
pci!PciReadDeviceConfig [d:\wmm1\drivers\busdrv\pci\config.c @ 349]:
fffff880`00f7b798 48895c2408      mov     qword ptr [rsp+8],rbx

PciReadDeviceSpace
pci!PciReadDeviceSpace [d:\wmm1\drivers\busdrv\pci\config.c @ 1621]:
fffff880`00f7c044 48895c2408      mov     qword ptr [rsp+8],rbx

...
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**! の\_各\_モジュール**](-for-each-module.md)

 

 






