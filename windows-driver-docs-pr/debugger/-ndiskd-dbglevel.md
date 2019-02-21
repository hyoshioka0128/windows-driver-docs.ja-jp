---
title: ndiskd.dbglevel
description: Ndiskd.dbglevel 拡張機能では、表示し、必要に応じて、現在の NDIS デバッグ レベルを変更します。 警告 ndiskd.dbglevel は、WPP とドライバーの検証ツールが提供されています。
ms.assetid: D134FD03-DABA-4558-A5C3-C365F77BD69A
keywords:
- デバッグ ndiskd.dbglevel Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.dbglevel
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7b9385a6ad354e28afccb0efded51abb748129cf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550727"
---
# <a name="ndiskddbglevel"></a>!ndiskd.dbglevel


**! Ndiskd.dbglevel**拡張機能が表示され、必要に応じて、現在の NDIS デバッグ レベルを変更します。

**警告**  
 **! ndiskd.dbglevel** WPP (Windows ソフトウェア トレース プリプロセッサ) とドライバーの検証ツールが提供されています。 ! ndiskd が表示されます、次の警告、ターゲット システムがサポートされていない場合 **! ndiskd.dbglevel**します。

```console
0: kd> !ndiskd.dbglevel
    This target does not support tracing through !ndiskd.dbglevel or
    !ndiskd.dbgsystems.
    Learn how to collect traces with WPP
```

場合は、警告の下部にあるリンクをクリックします。 ndiskd が詳細情報を提供します。

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

 

詳細については、WPP は、次を参照してください。 [WPP ソフトウェア トレース](https://msdn.microsoft.com/windows/hardware/drivers/devtest/wpp-software-tracing)します。

Driver Verifier についての詳細については、次を参照してください。 [Driver Verifier](https://msdn.microsoft.com/windows/hardware/drivers/devtest/driver-verifier)します。

WMI のトレースの詳細については、次を参照してください。 [WMI トレース拡張機能 (Wmitrace.dll)](https://msdn.microsoft.com/library/windows/hardware/ff561362)します。

```console
!ndiskd.dbglevel [-level <str>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-level______"></span><span id="_______-LEVEL______"></span> *-レベル*   
デバッグの詳細のレベル。 設定可能な値は、次のとおりです。

-   NONE - 無効にします。 デバッグ トレース
-   致命的なエラー - により印刷する致命的なエラー
-   エラー - 印刷するエラーを有効に
-   警告 - により警告印刷するには
-   情報 - により印刷する情報メッセージ
-   [詳細]-すべてのデバッグ トレースを印刷できます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="remarks"></a>注釈
-------

この拡張機能は、checked NDIS.sys のみに適用されます。 NDIS.sys のビルド情報を確認するには、実行、 [ **! ndiskd.ndis** ](-ndiskd-ndis.md)拡張機能。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ネットワーク ドライバーの設計ガイド](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista およびそれ以降のネットワーク リファレンス](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[ネットワーク スタックのデバッグ](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 拡張機能 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**!ndiskd.ndis**](-ndiskd-ndis.md)

[WPP ソフトウェア トレース](https://msdn.microsoft.com/windows/hardware/drivers/devtest/wpp-software-tracing)

[Driver Verifier](https://msdn.microsoft.com/windows/hardware/drivers/devtest/driver-verifier)

[WMI 拡張機能 (Wmitrace.dll) のトレース](https://msdn.microsoft.com/library/windows/hardware/ff561362)

 

 






