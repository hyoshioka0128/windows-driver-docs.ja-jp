---
title: ndiskd dbglevel
description: Ndiskd dbglevel 拡張機能が表示され、必要に応じて現在の NDIS デバッグレベルが変更されます。 警告 ndiskd dbglevel は、WPP およびドライバー検証ツールによって置き換えられました。
ms.assetid: D134FD03-DABA-4558-A5C3-C365F77BD69A
keywords:
- ndiskd dbglevel Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.dbglevel
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 95ee15b8bdeb654099ece0a7a94827be23cc20e1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837598"
---
# <a name="ndiskddbglevel"></a>!ndiskd.dbglevel


**! Ndiskd dbglevel**拡張機能が表示され、必要に応じて現在の NDIS デバッグレベルが変更されます。

**警告**  
 **! ndiskd DBGLEVEL**が WPP (Windows software trace プリプロセッサ) とドライバーの検証ツールによって置き換えられました。 ! ndiskd は、ターゲットシステムで **! ndiskd dbglevel**がサポートされていない場合に、次の警告を出します。

```console
0: kd> !ndiskd.dbglevel
    This target does not support tracing through !ndiskd.dbglevel or
    !ndiskd.dbgsystems.
    Learn how to collect traces with WPP
```

警告の下部にあるリンクをクリックすると、詳細情報が表示されます。

```console
0: kd> !ndiskd.help wpptracing
    WPP traces are fast, flexible, and detailed.  Plus, starting with Windows 8
    and Windows Server 2012, you can automatically decode NDIS traces using the
    symbol file.  Just point TraceView (or tracepdb.exe) at NDIS.PDB, and it
    will be able to get all the TMFs it needs to trace NDIS activity.
    
    If you would like traces to be printed in the debugger window, you use the
    !wmitrace extension.  For example, you might enable traces with this:

    !wmitrace.searchpath c:\path\to\TMF\files
    !wmitrace.start ndis -kd
    !wmitrace.enable ndis {DD7A21E6-A651-46D4-B7C2-66543067B869} -level 4 -flag 0x31f3
```

 

WPP の詳細については、「 [Wpp ソフトウェアのトレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)」を参照してください。

ドライバーの検証機能の詳細については、「 [Driver verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)」を参照してください。

WMI トレースの詳細については、「 [Wmi トレース拡張機能 (Wmitrace)](https://docs.microsoft.com/windows-hardware/drivers/debugger/wmi-tracing-extensions--wmitrace-dll-)」を参照してください。

```console
!ndiskd.dbglevel [-level <str>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______-level______"></span><span id="_______-LEVEL______"></span> *-レベルの*   
デバッグの詳細レベル。 設定可能な値は、次のとおりです。

-   NONE-デバッグトレースを無効にします
-   FATAL-致命的なエラーの出力を有効にします。
-   エラー-エラーの出力を有効にします
-   警告-警告の出力を有効にします
-   INFO-情報メッセージを出力できるようにします。
-   VERBOSE-すべてのデバッグトレースを出力できるようにします

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd .dll

<a name="remarks"></a>注釈
-------

この拡張機能は、チェックを行う NDIS にのみ適用されます。 NDIS のビルド情報を確認するには、 [ **! ndiskd ndis**](-ndiskd-ndis.md)拡張機能を実行します。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ネットワークドライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 以降のネットワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[ネットワークスタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd .dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

[ **!ndiskd.ndis**](-ndiskd-ndis.md)

[WPP ソフトウェア トレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)

[ドライバーの検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)

[WMI トレース拡張機能 (Wmitrace)](https://docs.microsoft.com/windows-hardware/drivers/debugger/wmi-tracing-extensions--wmitrace-dll-)

 

 






