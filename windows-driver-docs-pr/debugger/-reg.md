---
title: reg
description: Reg の拡張機能では、表示し、レジストリ データを検索します。
ms.assetid: 97944c84-da2e-4859-bf99-75d05413314d
keywords:
- reg の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- reg
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 15f071d84fa553899823c22d463db4ad51cd984d
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239491"
---
# <a name="reg"></a>!reg


**! Reg**拡張機能が表示され、レジストリ データを検索します。

```dbgcmd
!reg {querykey|q} FullKeyPath
!reg keyinfo HiveAddress KeyNodeAddress
!reg kcb Address 
!reg knode Address 
!reg kbody Address 
!reg kvalue Address 
!reg valuelist HiveAddress KeyNodeAddress 
!reg subkeylist HiveAddress KeyNodeAddress  
!reg baseblock HiveAddress 
!reg seccache HiveAddress 
!reg hashindex [HiveAddress]HashKey
!reg openkeys {HiveAddress|0}
!reg openhandles {HiveAddress|0} 
!reg findkcb FullKeyPath 
!reg hivelist 
!reg viewlist HiveAddress 
!reg freebins HiveAddress 
!reg freecells BinAddress 
!reg dirtyvector HiveAddress 
!reg cellindex HiveAddress Index
!reg freehints HiveAddress Storage Display 
!reg translist {RmAddress|0}
!reg uowlist TransactionAddress
!reg locktable KcbAddress ThreadAddress
!reg convkey KeyPath
!reg postblocklist
!reg notifylist
!reg ixlock LockAddress
!reg dumppool [s|r]
```

## <a name="span-idddkregdbgspanspan-idddkregdbgspanparameters"></a><span id="ddk__reg_dbg"></span><span id="DDK__REG_DBG"></span>パラメーター


<span id="_______querykeyq_FullKeyPath______"></span><span id="_______querykeyq_fullkeypath______"></span><span id="_______QUERYKEYQ_FULLKEYPATH______"></span> {**querykey**|**q**} **** *FullKeyPath*   
キーがキャッシュされている場合は、キーのサブキーおよび値を表示します。 *FullKeyPath*完全なキーのパスを指定します。

<span id="_____________keyinfo_HiveAddress_KeyNodeAddress"></span><span id="_____________keyinfo_hiveaddress_keynodeaddress"></span><span id="_____________KEYINFO_HIVEADDRESS_KEYNODEADDRESS"></span> **keyinfo** *HiveAddress* **** *KeyNodeAddress*  
サブキーとキーのノードの値が表示されます。 *HiveAddress*ハイブのアドレスを指定します。 *KeyNodeAddress*キー ノードのアドレスを指定します。

<span id="_______kcb_______Address______"></span><span id="_______kcb_______address______"></span><span id="_______KCB_______ADDRESS______"></span> **kcb** **** *アドレス*   
レジストリ キーの制御ブロックが表示されます。 *アドレス*キー コントロール ブロックのアドレスを指定します。

<span id="_______knode_______Address______"></span><span id="_______knode_______address______"></span><span id="_______KNODE_______ADDRESS______"></span> **knode** **** *アドレス*   
レジストリ キーのノードの構造を表示します。 *アドレス*キー ノードのアドレスを指定します。

<span id="_______kbody_______Address______"></span><span id="_______kbody_______address______"></span><span id="_______KBODY_______ADDRESS______"></span> **kbody** **** *アドレス*   
レジストリ キーの本文の構造体を表示します。 *アドレス*キーの本文のアドレスを指定します。 (レジストリ キーの本文は、ハンドルに関連付けられている実際のオブジェクトです)。

<span id="_______kvalue_______Address______"></span><span id="_______kvalue_______address______"></span><span id="_______KVALUE_______ADDRESS______"></span> **kvalue** **** *アドレス*   
レジストリ キーの値の構造を表示します。 *アドレス*値のアドレスを指定します。

<span id="_______valuelist_______HiveAddress_KeyNodeAddress______"></span><span id="_______valuelist_______hiveaddress_keynodeaddress______"></span><span id="_______VALUELIST_______HIVEADDRESS_KEYNODEADDRESS______"></span> **valuelist** **** *HiveAddress* **** *KeyNodeAddress*   
指定したキー ノード値の一覧を表示します。 *HiveAddress*ハイブのアドレスを指定します。 *KeyNodeAddress*キー ノードのアドレスを指定します。

<span id="subkeylist_______HiveAddress_KeyNodeAddress______"></span><span id="subkeylist_______hiveaddress_keynodeaddress______"></span><span id="SUBKEYLIST_______HIVEADDRESS_KEYNODEADDRESS______"></span>**subkeylist** **** *HiveAddress* **** *KeyNodeAddress*   
指定したキーのノードのサブキーの一覧を表示します。 *HiveAddress*ハイブのアドレスを指定します。 *KeyNodeAddress*キー ノードのアドレスを指定します。

<span id="_______baseblock_______HiveAddress______"></span><span id="_______baseblock_______hiveaddress______"></span><span id="_______BASEBLOCK_______HIVEADDRESS______"></span> **baseblock** **** *HiveAddress*   
Hive の基本ブロックが表示されます (とも呼ばれる、 *hive ヘッダー*)。 *HiveAddress*ハイブのアドレスを指定します。

<span id="_______seccache_______HiveAddress______"></span><span id="_______seccache_______hiveaddress______"></span><span id="_______SECCACHE_______HIVEADDRESS______"></span> **seccache** **** *HiveAddress*   
Hive のセキュリティのキャッシュを表示します。 *HiveAddress*ハイブのアドレスを指定します。

<span id="_______hashindex_______HiveAddress_HashKey______"></span><span id="_______hashindex_______hiveaddress_hashkey______"></span><span id="_______HASHINDEX_______HIVEADDRESS_HASHKEY______"></span> **hashindex** **** \[*HiveAddress*\] **** *HashKey*   
ハッシュ キーのハッシュ インデックスのエントリを計算します。 *HiveAddress*ハイブのアドレスを指定します。 *HashKey*キーを指定します。

**注***HiveAddress* 7 以降、ターゲット コンピューターは Windows を実行している場合は必須です。



<span id="_______openkeys_HiveAddress0_"></span><span id="_______openkeys_hiveaddress0_"></span><span id="_______OPENKEYS_HIVEADDRESS0_"></span> **openkeys** {*HiveAddress*|**0**}   
Hive では、すべての開いているキーを表示します。 *HiveAddress*ハイブのアドレスを指定します。 0 を代わりに使用する場合は、レジストリ全体のハッシュ テーブルが表示されます。このテーブルには、レジストリ内の開いているすべてのキーが含まれています。

<span id="_______findkcb_______FullKeyPath______"></span><span id="_______findkcb_______fullkeypath______"></span><span id="_______FINDKCB_______FULLKEYPATH______"></span> **findkcb** **** *FullKeyPath*   
レジストリ パスに対応するレジストリ キーの制御ブロックが表示されます。 *FullKeyPath*完全なキーのパスを指定します。 このパスはハッシュ テーブルに存在する必要があります。

<span id="_______hivelist______"></span><span id="_______HIVELIST______"></span> **hivelist**   
各 hive に関する詳細情報と共に、システムでは、ハイブのすべての一覧を表示します。

<span id="_______viewlist_______HiveAddress______"></span><span id="_______viewlist_______hiveaddress______"></span><span id="_______VIEWLIST_______HIVEADDRESS______"></span> **viewlist** **** *HiveAddress*   
すべて固定およびビューごとに詳細な情報を hive ビューのマップを表示します。 *HiveAddress*ハイブのアドレスを指定します。

<span id="_______freebins_______HiveAddress______"></span><span id="_______freebins_______hiveaddress______"></span><span id="_______FREEBINS_______HIVEADDRESS______"></span> **freebins** **** *HiveAddress*   
各ビンの詳細な情報をハイブの無料のビンのすべてを表示します。 *HiveAddress*ハイブのアドレスを指定します。

<span id="_______freecells_______BinAddress______"></span><span id="_______freecells_______binaddress______"></span><span id="_______FREECELLS_______BINADDRESS______"></span> **freecells** **** *BinAddress*   
ビンを反復処理し、その中のすべてのフリー セルを表示します。 *BinAddress*箱のアドレスを指定します。

<span id="_______dirtyvector_______HiveAddress______"></span><span id="_______dirtyvector_______hiveaddress______"></span><span id="_______DIRTYVECTOR_______HIVEADDRESS______"></span> **dirtyvector** **** *HiveAddress*   
Hive のダーティ ベクトルを表示します。 *HiveAddress*ハイブのアドレスを指定します。

<span id="_______cellindex_______HiveAddress_Index______"></span><span id="_______cellindex_______hiveaddress_index______"></span><span id="_______CELLINDEX_______HIVEADDRESS_INDEX______"></span> **cellindex** **** *HiveAddress* **** *Index*   
Hive では、セルの仮想アドレスを表示します。 *HiveAddress*ハイブのアドレスを指定します。 *インデックス*セル インデックスを指定します。

<span id="_____________freehints_HiveAddress_Storage_Display"></span><span id="_____________freehints_hiveaddress_storage_display"></span><span id="_____________FREEHINTS_HIVEADDRESS_STORAGE_DISPLAY"></span> **freehints** *HiveAddress* **** *ストレージ* **** *表示*  
無料のヒント情報を表示します。

<span id="_____________translist_RmAddress0"></span><span id="_____________translist_rmaddress0"></span><span id="_____________TRANSLIST_RMADDRESS0"></span> **translist** {*RmAddress*|**0**}  
RM でアクティブなトランザクションの一覧を表示します。 *RmAddress* RM のアドレスを指定します

<span id="_____________uowlist_TransactionAddress"></span><span id="_____________uowlist_transactionaddress"></span><span id="_____________UOWLIST_TRANSACTIONADDRESS"></span> **uowlist** *TransactionAddress*  
トランザクションにアタッチされている UoWs の一覧が表示されます。 *TransactionAddress*トランザクションのアドレスを指定します。

<span id="_____________locktable_KcbAddress_ThreadAddress"></span><span id="_____________locktable_kcbaddress_threadaddress"></span><span id="_____________LOCKTABLE_KCBADDRESS_THREADADDRESS"></span> **locktable** *KcbAddress* *ThreadAddress*  
関連するロックのテーブルの内容を表示します。

<span id="_____________convkey_KeyPath"></span><span id="_____________convkey_keypath"></span><span id="_____________CONVKEY_KEYPATH"></span> **convkey** *KeyPath*  
キーのパスのハッシュ キーを表示します。

<span id="_____________postblocklist"></span><span id="_____________POSTBLOCKLIST"></span> **postblocklist**  
Postblocks 投稿が含まれるスレッドの一覧が表示されます。

<span id="_____________notifylist"></span><span id="_____________NOTIFYLIST"></span> **notifylist**  
システム内のブロックの通知の一覧を表示します。

<span id="_____________ixlock_LockAddress"></span><span id="_____________ixlock_lockaddress"></span><span id="_____________IXLOCK_LOCKADDRESS"></span> **ixlock** *LockAddress*  
インテント ロックの所有権を表示します。 *LockAddress*ロックのアドレスを指定します。

<span id="_______dumppool_sr"></span><span id="_______DUMPPOOL_SR"></span> **dumppool** \[ **s**|**r**\]  
レジストリに割り当てられた表示ページ プール 場合**s**を指定すると、レジストリのページの一覧は、一時ファイルに保存されます。 場合**r**を指定すると、レジストリのページの一覧は、以前に保存した一時ファイルから復元されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

レジストリとそのコンポーネントについては、次を参照してください。 *Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 

<a name="remarks"></a>注釈
-------

次に例を示します。 まずを使用して **! reg hivelist** hive アドレスの一覧を取得します。

```dbgcmd
00: kd> !reg hivelist
## 

## |     HiveAddr     |Stable Length|    Stable Map    |Volatile Length|    Volatile Map    |MappedViews|PinnedViews|U(Cnt)|     BaseBlock     | FileName 

| fffff8a000014010 |       1000  | fffff8a0000140b0 |       1000    |  fffff8a000014328  |     0| fffff8a00001e000  | <NONAME>
| fffff8a000028010 |     a15000  | fffff8a00002e000 |      1a000    |  fffff8a000028328  |     0| fffff8a000029000  | SYSTEM
| fffff8a00004f010 |      14000  | fffff8a00004f0b0 |       c000    |  fffff8a00004f328  |     0| fffff8a000050000  | <NONAME>
| fffff8a000329010 |       6000  | fffff8a0003290b0 |          0    |  0000000000000000  |     0| fffff8a00032f000  | Device\HarddiskVolume1\Boot\BCD
| fffff8a0002f2010 |    4255000  | fffff8a0006fa000 |       6000    |  fffff8a0002f2328  |     0| fffff8a00036c000  | emRoot\System32\Config\SOFTWARE
| fffff8a000df0010 |      f7000  | fffff8a000df00b0 |       1000    |  fffff8a000df0328  |     0| fffff8a000df1000  | temRoot\System32\Config\DEFAULT
| fffff8a0010f8010 |       9000  | fffff8a0010f80b0 |       1000    |  fffff8a0010f8328  |     0| fffff8a0010f9000  | emRoot\System32\Config\SECURITY
| fffff8a001158010 |       7000  | fffff8a0011580b0 |          0    |  0000000000000000  |     0| fffff8a001159000  | \SystemRoot\System32\Config\SAM
| fffff8a00124b010 |      24000  | fffff8a00124b0b0 |          0    |  0000000000000000  |     0| fffff8a00124c000  | files\NetworkService\NTUSER.DAT
| fffff8a0012df220 |      b7000  | fffff8a0012df2c0 |          0    |  0000000000000000  |     0| fffff8a0012e6000  | \SystemRoot\System32\Config\BBI
| fffff8a001312220 |      26000  | fffff8a0013122c0 |          0    |  0000000000000000  |     0| fffff8a00117e000  | rofiles\LocalService\NTUSER.DAT
| fffff8a001928010 |      64000  | fffff8a0019280b0 |       3000    |  fffff8a001928328  |     0| fffff8a00192b000  | User.MYTESTCOMPUTER2\ntuser.dat
| fffff8a001b9b010 |     203000  | fffff8a001bc4000 |          0    |  0000000000000000  |     0| fffff8a001b9c000  | \Microsoft\Windows\UsrClass.dat
| fffff8a001dc0010 |      30000  | fffff8a001dc00b0 |          0    |  0000000000000000  |     0| fffff8a001dc2000  | Volume Information\Syscache.hve
## | fffff8a0022dc010 |     175000  | fffff8a0022dc0b0 |          0    |  0000000000000000  |     0| fffff8a0022dd000  | \AppCompat\Programs\Amcache.hve
```

上記の出力 (fffff8a00004f010) で 3 番目の hive のアドレスを使用してへの引数として **! reg openkeys**します。

```dbgcmd
0: kd> !reg openkeys fffff8a00004f010

# Hive: \REGISTRY\MACHINE\HARDWARE

Index e9:    3069276d kcb=fffff8a00007eb98 cell=00000220 f=00200000 \REGISTRY\MACHINE\HARDWARE\DESCRIPTION\SYSTEM
Index 101:   292eea1f kcb=fffff8a00007ecc0 cell=000003b8 f=00200000 \REGISTRY\MACHINE\HARDWARE\DESCRIPTION\SYSTEM\MULTIFUNCTIONADAPTER
Index 140:   d927b0d4 kcb=fffff8a00007ea70 cell=000001a8 f=00200000 \REGISTRY\MACHINE\HARDWARE\DESCRIPTION
Index 160:   96d26a30 kcb=fffff8a00007e6f8 cell=00000020 f=002c0000 \REGISTRY\MACHINE\HARDWARE

# 0x4 keys found
```

最初の完全なキー パスを使用して、上記の出力 (\\レジストリ\\マシン\\ハードウェア\\説明\\システム) への引数として **! reg querykey**します。

```dbgcmd
0: kd> !reg querykey \REGISTRY\MACHINE\HARDWARE\DESCRIPTION\SYSTEM

Found KCB = fffff8a00007eb98 :: \REGISTRY\MACHINE\HARDWARE\DESCRIPTION\SYSTEM

Hive         fffff8a00004f010
KeyNode      fffff8a000054224

[SubKeyAddr]         [SubKeyName]
fffff8a000060244     CentralProcessor
fffff8a00006042c     FloatingPointProcessor
fffff8a0000543bc     MultifunctionAdapter

[SubKeyAddr]         [VolatileSubKeyName]
fffff8a000338d8c     BIOS
fffff8a0002a2e4c     VideoAdapterBusses

 Use '!reg keyinfo fffff8a00004f010 <SubKeyAddr>' to dump the subkey details

[ValueType]         [ValueName]                   [ValueData]
REG_BINARY          Component Information         0x542AC - 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
REG_SZ              Identifier                    AT/AT COMPATIBLE
REG_FULL_RESOURCE_DESCRIPTORConfiguration Data            ff ff ff ff ff ff ff ff 00 00 00 00 02 00 00 00 05 00 00 00 18 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 80 00 ff 03 00 00 3f 00 fe 00 02 00 81 00 fe 03 00 00 3f 00 fe 00 02 00 05 00 00 00 08 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 0c 00 00 00 04 00 
REG_SZ              SystemBiosDate                07/18/07
REG_MULTI_SZ        SystemBiosVersion             HPQOEM - 20070718\0\0
REG_SZ              VideoBiosDate                 03/23/20
REG_MULTI_SZ        VideoBiosVersion              Hardware Version 0.0\0\0
```

別の例を次に示します。

```dbgcmd
kd> !reg hivelist
## 

## | HiveAddr |Stable Length|Stable Map|Volatile Length|Volatile Map|MappedViews|PinnedViews|U(Cnt)| BaseBlock | FileName 

| e16e7428 |       2000  | e16e7484 |          0    |  00000000  |        1  |        0  |     0| e101f000  | \Microsoft\Windows\UsrClass.dat
| e1705a78 |      77000  | e1705ad4 |       1000    |  e1705bb0  |       30  |        0  |     0| e101c000  | ttings\Administrator\ntuser.dat
| e13d4b88 |     814000  | e146a000 |       1000    |  e13d4cc0  |      255  |        0  |     0| e1460000  | emRoot\System32\Config\SOFTWARE
| e13ad008 |      23000  | e13ad064 |       1000    |  e13ad140  |        9  |        0  |     0| e145e000  | temRoot\System32\Config\DEFAULT
| e13b3b88 |       a000  | e13b3be4 |       1000    |  e13b3cc0  |        3  |        0  |     0| e145d000  | emRoot\System32\Config\SECURITY
| e142d008 |       5000  | e142d064 |          0    |  00000000  |        2  |        0  |     0| e145f000  | <UNKNOWN>
| e11e3628 |       4000  | e11e3684 |       3000    |  e11e3760  |        0  |        0  |     0| e11e4000  | <NONAME>
| e10168a8 |     1c1000  | e1016904 |      15000    |  e10169e0  |       66  |        0  |     0| e1017000  | SYSTEM
## | e10072c8 |       1000  | e1007324 |          0    |  00000000  |        0  |        0  |     0| e1010000  | <NONAME>


kd> !reg hashindex e16e7428

CmpCacheTable = e100a000

Hash Index[e16e7428] : 5ac
Hash Entry[e16e7428] : e100b6b0

kd> !reg openkeys e16e7428

Index 68:  7bab7683 kcb=e13314f8 cell=00000740 f=00200004 \REGISTRY\USER\S-1-5-21-1715567821-413027322-527237240-500_Classes\CLSID
Index 7a1:  48a30288 kcb=e13a3738 cell=00000020 f=002c0004 \REGISTRY\USER\S-1-5-21-1715567821-413027322-527237240-500_Classes
```

書式設定されたレジストリ キーの情報を表示するには、使用、 [ **! dreg** ](-dreg.md)拡張子代わりにします。









