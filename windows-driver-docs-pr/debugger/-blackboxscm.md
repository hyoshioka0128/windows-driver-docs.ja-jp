---
title: blackboxscm
description: Blackboxscmextension には、サービス コントロール マネージャー (scm) セカンダリのブート データが表示されます。
keywords:
- Windows デバッグ blackboxscm
ms.author: windowsdriverdev
ms.date: 01/02/2019
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- blackboxscm
api_type:
- NA
ms.openlocfilehash: ccd8d70b2c02a57c6a280fa0bd7c61cb406cfc83
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334678"
---
# <a name="blackboxscm"></a>!blackboxscm

**! Blackboxscm**拡張機能では、カーネル モードのダンプ ファイルで入手可能なサービス コントロール マネージャー (SCM) からの情報が表示されます。 拡張機能は、未処理のサービス制御要求のあるすべてのサービスの名前で表示されます。    バグチェックが発生し、常に使用できない時点で保存されたカーネル モードのダンプにキャッシュされたデータから情報が取得されます。


構文

```dbgcmd
!blackboxscm  
```

## <a name="span-idparametersspanparameters"></a><span id="Parameters"></span>パラメーター

*None*   


## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ext.dll


## <a name="span-idremarksspanremarks"></a><span id="Remarks"></span>「解説」

コマンドが、特定のサービスの LPHANDLER_FUNCTION_EX コールバック関数にディスパッチされました。  
優秀では、通常のシャット ダウンまたはコンピューターの再起動、SERVICE_CONTROL_SHUTDOWN または SERVICE_CONTROL_PRESHUTDOWN を遅らせるでしたなどを要求します。

### <a name="example-command-output"></a>コマンドの出力の例 

多くのダンプ ファイルに 1 つのサービスだけが返されます。

```dbgcmd
2: kd> !ext.blackboxscm
    Name: gpsvc
    Code: 15
```

返されるデータは、2 つのフィールドについてを説明します。

*名前*のダンプが発生した時刻にアクティブだったサービスの名前。

*コード*-未処理である dwControl、10 進数値

この例では、15 (または 0x0000000F) コードが SERVICE_CONTROL_PRESHUTDOWN として定義されます。


### <a name="multiple-services"></a>複数のサービス

複数のサービスが一覧表示されますが表示されている最初のサービスのみ失敗の分析用の通常です。  これは、これらの要求を最初のサービスが実際には、制御要求を受信しただけの SCM (サービス コントロール マネージャー) が連続的に待機するためです。

SCM の詳細については、次を参照してください。[サービス コントロール マネージャー](https://docs.microsoft.com/en-us/windows/desktop/Services/service-control-manager)します。


### <a name="span-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span>追加情報

dwControl 値が winsvc.h で定義されているし、パラメーターとして記載されている[LPHANDLER_FUNCTION_EX コールバック関数](https://docs.microsoft.com/windows/desktop/api/winsvc/nc-winsvc-lphandler_function_ex#parameters)します。

 


