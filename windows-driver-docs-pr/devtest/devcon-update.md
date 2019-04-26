---
title: DevCon Update
description: 強制的に指定したデバイスの現在のデバイス ドライバーをドライバーの INF ファイルに指定されたに置き換えます。 ローカル コンピューターでのみ有効です。
ms.assetid: c07d7abe-31d8-4a8d-87da-8db649710c15
keywords:
- DevCon 更新ドライバーの開発ツール
topic_type:
- apiref
api_name:
- DevCon Update
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2922b2e9a0cd45183bf56d1b4145437133f1d956
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346997"
---
# <a name="devcon-update"></a>DevCon Update


強制的に指定したデバイスの現在のデバイス ドライバーをドライバーの INF ファイルに指定されたに置き換えます。 ローカル コンピューターでのみ有効です。

```
    devcon [/r] update INFfile HardwareID 
```

## <a name="span-idddkdevconupdatetoolsspanspan-idddkdevconupdatetoolsspanparameters"></a><span id="ddk_devcon_update_tools"></span><span id="DDK_DEVCON_UPDATE_TOOLS"></span>パラメーター


<span id="________r______"></span><span id="________R______"></span> **/r**   
条件付き再起動します。 再起動が必要な変更を有効にする場合にのみ操作を完了した後、システムを再起動します。

<span id="_______INFfile______"></span><span id="_______inffile______"></span><span id="_______INFFILE______"></span> *INFfile*   
更新プログラムで使用される INF (情報) ファイルの完全なパスとファイル名を指定します。 パスを省略した場合、DevCon ファイルが現在のディレクトリがある前提としています。

<span id="_______HardwareID______"></span><span id="_______hardwareid______"></span><span id="_______HARDWAREID______"></span> *HardwareID*   
指定されたハードウェア ID を持つデバイスのドライバーの更新プログラム このコマンドで指定されたハードウェア ID では、デバイスのハードウェア ID を完全に一致する必要があります。 パターンが有効ではありません。 単一引用符文字を入力しないでください (**'**) をリテラル値を示します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

**DevCon 更新**操作は、それらのドライバーが古いまたは最新のドライバーや別の INF ファイル内のドライバーよりも小さい適切な場合でも、指定した INF ファイルで最も適切なドライバーを更新を強制します。 詳細については、次を参照してください。[セットアップによるドライバーの選択](https://msdn.microsoft.com/library/windows/hardware/ff546228)します。

使用することはできません、 **DevCon 更新**存在デバイス用のドライバーを更新するコマンド。

任意のデバイスのドライバーを更新する前に、デバイスは、更新コマンドによって影響を受けるを決定します。 表示のコマンドで使用して、ハードウェア ID をなどを行うに[ **DevCon HwIDs** ](devcon-hwids.md)または[ **DevCon DriverFiles**](devcon-driverfiles.md)します。 特に重要になります、 **DevCon 更新**操作 DevCon に更新するデバイス ドライバーが表示されないためです。

DevCon では、INF ファイルは未署名のドライバを指定する場合、またはリムーバブル メディア上のドライバー ファイルなどの必要なファイルを見つけられない場合、ユーザーが求められます。 応答を要求するプロンプトを抑制する非対話型の更新操作を使用して、 [ **DevCon UpdateNI**](devcon-updateni.md)します。

システムは、この変更を有効にするを再起動する必要があります。 DevCon システムを再起動するのには、再起動の条件付きパラメーターを追加します (/r) コマンド。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>サンプルの使用法

```
devcon update c:\windows\inf\newdvc.inf ISAPNP\CSC4324\0
devcon /r update c:\windows\inf\newdvc.inf *PNP030b
```

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

[例: 32:通信ポートのドライバーを更新します。](devcon-examples.md#ddk_example_32_update_the_driver_for_communication_ports_tools)

[例 44:HAL を強制的に更新します。](devcon-examples.md#ddk_example_44_forcibly_update_the_hal_tools)









