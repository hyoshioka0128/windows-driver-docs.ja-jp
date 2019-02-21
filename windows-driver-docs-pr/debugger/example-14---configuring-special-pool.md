---
title: 構成の特別なプールの 14 の例
description: 構成の特別なプールの 14 の例
ms.assetid: a89f8a08-30e4-4d04-9689-c665b2175780
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: c70d2bb2345c4378c2cf2214510ffecfb7250585
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535867"
---
# <a name="example-14-configuring-special-pool"></a>14 の使用例:特別なプールを構成します。


Windows vista 以降、構成できます、[特別なプール](special-pool.md)カーネル フラグを設定またはレジストリ設定として機能します。 をカーネル (実行時) フラグの設定として構成する場合は、変更を有効にするコンピューターを再起動する必要はありません。 以前のバージョンの Windows では、特別なプールはレジストリ設定としてのみ使用できます。

また、以降 Windows Vista では、設定して、コマンドラインからの特別なプール機能を構成します。 Windows の以前のバージョンでは、設定し、グローバル フラグのダイアログ ボックスでのみ特別なプール機能を構成します。

### <a name="span-idrequestspecialpoolbypooltagwithoutrebootingspanspan-idrequestspecialpoolbypooltagwithoutrebootingspanrequest-special-pool-by-pool-tag-without-rebooting"></a><span id="request_special_pool_by_pool_tag_without_rebooting"></span><span id="REQUEST_SPECIAL_POOL_BY_POOL_TAG_WITHOUT_REBOOTING"></span>プール タグを使用して再起動しなくても特別なプールを要求します。

次のコマンドですべての割り当て用の特別なプールの要求、 **Tag1**プール タグ。 この設定が、すぐに有効になりますが、シャット ダウン、または Windows を再起動する場合に失われます。

このコマンドを使用して、 **/k**カーネル (実行時) フラグ設定を指定するパラメーター、および + spp の省略形を特別なプールの要求を設定します。

```console
gflags /k +spp Tag1
```

Gflags は、印刷することで応答します。

```console
Special Pool set to 0x31676154
PoolTagOverruns set to 0x1
Current Running Kernel Settings are: 00000000
```

特別なプールの割り当て要求がカーネル フラグの設定ではなく、カーネル設定の値に反映されていないことに注意してください。

また、特別なプールの割り当て要求オーバーラン (0x1) の値を変更したりしないアンダーラン特別なプール (0x0) 設定。 オーバーランから変更するには、既定値は、アンダーランには、Gflags ダイアログを使用します。 詳しくは、次を参照してください。[オーバーランの検出とアンダーラン](detecting-overruns-and-underruns.md)します。

コマンドラインでプール タグを表示することはできません。 プール タグがカーネル設定であることを確認するには、Gflags のダイアログ ボックスを使用します。

### <a name="span-idrequestspecialpoolbypooltagintheregistryspanspan-idrequestspecialpoolbypooltagintheregistryspanrequest-special-pool-by-pool-tag-in-the-registry"></a><span id="request_special_pool_by_pool_tag_in_the_registry"></span><span id="REQUEST_SPECIAL_POOL_BY_POOL_TAG_IN_THE_REGISTRY"></span>レジストリのプール タグで特別なプールを要求します。

次のコマンドですべての割り当て用の特別なプールの要求、 **Tag1**プール タグ。 この設定はレジストリに格納されている、ためを行うため、コンピューターを再起動する必要がありますが、変更するまでは有効。

このコマンドを使用して、 **/r**レジストリ設定を指定するパラメーター、および + spp の省略形を特別なプールの要求を設定します。

```console
gflags /r +spp Tag1
```

Gflags は、印刷することで応答します。

```console
Special Pool set to 0x31676154
PoolTagOverruns set to 0x1
Current Boot Registry Settings are: 00000000
```

特別なプールの割り当て要求がレジストリ フラグの設定ではなく、レジストリ設定の値に反映されていないことに注意してください。

また、特別なプールの割り当て要求オーバーラン (0x1) の値を変更したりしないアンダーラン特別なプール (0x0) 設定。 オーバーランから変更するには、既定値は、アンダーランには、Gflags ダイアログを使用します。 詳しくは、次を参照してください。[オーバーランの検出とアンダーラン](detecting-overruns-and-underruns.md)します。

値がレジストリに追加されたことを確認するの値を表示する Reg または Regedit を使用、 **PoolTag**内のエントリ、 **HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\セッション マネージャー\\メモリ管理**キー。

次に、例を示します。

```console
c:>reg query "HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management" -v PoolTag
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management
    PoolTag    REG_DWORD    0x31676154
```

### <a name="span-idrequestspecialpoolbysizewithoutrebootingspanspan-idrequestspecialpoolbysizewithoutrebootingspanrequest-special-pool-by-size-without-rebooting"></a><span id="request_special_pool_by_size_without_rebooting"></span><span id="REQUEST_SPECIAL_POOL_BY_SIZE_WITHOUT_REBOOTING"></span>サイズを再起動しなくても特別なプールを要求します。

次のコマンドは、x86 では 1 から 8 バイトの割り当てのための特別なプールを要求、ページを使用してコンピューター\_0x1000 のサイズと 8 バイトの割り当ての粒度。

このコマンドを使用して、 **/k**カーネル (実行時) フラグ設定を指定するパラメーター、および + spp の省略形を特別なプールの要求を設定します。 サイズの値には、サイズ、プール タグではありませんがあることを示す 0 x が付きます。

値、合計で 16 バイト (0x10) の範囲 (8 バイト) の最大サイズには、0x10 を割り当ての粒度 (8 バイト) を加算して計算されます。 入力する適切な値を確認するのには、「an 割り当てサイズを選択する」を参照してください[特別なプール](special-pool.md)します。

```console
gflags /k +spp 0x10
```

Gflags は、印刷することで応答します。

```console
Special Pool set to 0x10
PoolTagOverruns set to 0x1
Current Running Kernel Settings are: 00000000
```

ここでも、特別なプールの割り当て要求はカーネル フラグの設定ではありませんし、カーネル設定の値には反映されません。

また、特別なプールの割り当て要求オーバーラン (0x1) の値を変更したりしないアンダーラン特別なプール (0x0) 設定。 オーバーランから変更するには、既定値は、アンダーランには、Gflags ダイアログを使用します。 詳しくは、次を参照してください。[オーバーランの検出とアンダーラン](detecting-overruns-and-underruns.md)します。

### <a name="span-idrequestspecialpoolbysizeintheregistryspanspan-idrequestspecialpoolbysizeintheregistryspanrequest-special-pool-by-size-in-the-registry"></a><span id="request_special_pool_by_size_in_the_registry"></span><span id="REQUEST_SPECIAL_POOL_BY_SIZE_IN_THE_REGISTRY"></span>レジストリのサイズで特別なプールを要求します。

次のコマンドは、x64 1040 を 1024 バイトの割り当てのための特別なプールを要求、ページを使用してコンピューター\_0x1000 のサイズと 16 バイトの割り当ての粒度。

このコマンドを使用して、 **/r**システム全体のレジストリ設定を指定するパラメーター、および + spp の省略形を特別なプールの要求を設定します。 サイズの値には、サイズ、プール タグではありませんがあることを示す 0 x が付きます。

0x420 の値は、合計 1056 バイト (0x420) の範囲 (1040 バイト) の最大サイズに割り当ての粒度 (16 バイト) を加算して計算されます。 入力する適切な値を確認するのには、「an 割り当てサイズを選択する」を参照してください[特別なプール](special-pool.md)します。

```console
gflags /r +spp 0x420
```

Gflags は、印刷することで応答します。

```console
Special Pool set to 0x420
PoolTagOverruns set to 0x1
Current Boot Registry Settings are: 00000000
```

ここでも、特別なプールの割り当て要求はレジストリ フラグの設定ではありませんし、レジストリ設定の値には反映されません。

また、特別なプールの割り当て要求オーバーラン (0x1) の値を変更したりしないアンダーラン特別なプール (0x0) 設定。 オーバーランから変更するには、既定値は、アンダーランには、Gflags ダイアログを使用します。 詳しくは、次を参照してください。[オーバーランの検出とアンダーラン](detecting-overruns-and-underruns.md)します。

値がレジストリに追加されたことを確認するの値を表示する Reg または Regedit を使用、 **PoolTag**内のエントリ、 **HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\セッション マネージャー\\メモリ管理**キー。

次に、例を示します。

```console
c:>reg query "HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management" -v PoolTag
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management
    PoolTag    REG_DWORD    0x420
```

### <a name="span-idcancelaspecialpoolrequestspanspan-idcancelaspecialpoolrequestspancancel-a-special-pool-request"></a><span id="cancel_a_special_pool_request"></span><span id="CANCEL_A_SPECIAL_POOL_REQUEST"></span>特別なプールの要求をキャンセルします。

次のコマンドは、カーネル (実行時) フラグの設定として、特別なプールの要求をキャンセルします。 コマンドは、サイズ、プール タグを使用して要求を同じです。

```console
gflags /k -spp
```

次のコマンドは、レジストリ設定として、特別なプールの要求をキャンセルします。 コマンドは、サイズ、プール タグを使用して要求を同じです。

```console
gflags /r -spp
```

コマンドが成功したら、Gflags は印刷することで応答します。

```console
Special Pool value has been deleted.
```

 

 





