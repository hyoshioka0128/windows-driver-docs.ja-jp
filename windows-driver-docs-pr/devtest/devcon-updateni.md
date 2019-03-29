---
title: DevCon UpdateNI
description: 情報または確認を求めることがなく、指定した INF ファイルに表示されているドライバーと現在のデバイス ドライバーを強制的に置き換えられます。 ローカル コンピューターでのみ有効です。
ms.assetid: 436a9731-1c61-4b38-b145-7012da55b699
keywords:
- DevCon UpdateNI ドライバーの開発ツール
topic_type:
- apiref
api_name:
- DevCon UpdateNI
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d059242dd4129a38c7052712e0c32fb08de9bc12
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577860"
---
# <a name="devcon-updateni"></a>DevCon UpdateNI


情報または確認を求めることがなく、指定した INF ファイルに表示されているドライバーと現在のデバイス ドライバーを強制的に置き換えられます。 ローカル コンピューターでのみ有効です。

```
    devcon [/r] updateni INFfile HardwareID 
```

## <a name="span-idddkdevconupdatenitoolsspanspan-idddkdevconupdatenitoolsspanparameters"></a><span id="ddk_devcon_updateni_tools"></span><span id="DDK_DEVCON_UPDATENI_TOOLS"></span>パラメーター


<span id="________r______"></span><span id="________R______"></span> **/r**   
条件付き再起動します。 再起動が必要な変更を有効にする場合にのみ操作を完了した後、システムを再起動します。

<span id="_______INFfile______"></span><span id="_______inffile______"></span><span id="_______INFFILE______"></span> *INFfile*   
デバイスの INF (情報) ファイルの完全なパスとファイル名を指定します。 パスを省略した場合、DevCon ファイルが現在のディレクトリがある前提としています。

<span id="_______HardwareID______"></span><span id="_______hardwareid______"></span><span id="_______HARDWAREID______"></span> *HardwareID*   
デバイスのハードウェア ID を指定します。

指定されたハードウェア ID では、デバイスのハードウェア ID を完全に一致する必要があります。 パターンが有効ではありません。 単一引用符文字を入力しないでください (**'**) をリテラル値を示します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

**DevCon UpdateNI**操作応答を要求するすべてのユーザー メッセージを非表示にし、既定の応答を前提としています。 結果として、この操作を使用して署名されていないドライバーをインストールすることはできません。 更新中にユーザー プロンプトを表示する使用[ **DevCon 更新**](devcon-update.md)します。

**DevCon UpdateNI**操作に指定した INF ファイルのドライバーが古いまたは最新のドライバーよりも小さい適切な場合でも、更新を強制しています。

任意のデバイスのドライバーを更新する前に、デバイスは、更新コマンドによって影響を受けるを決定します。 表示のコマンドで使用して、ハードウェア ID をなどを行うに[ **DevCon HwIDs** ](devcon-hwids.md)または[ **DevCon DriverFiles**](devcon-driverfiles.md)します。 これはで特に重要です、 **DevCon UpdateNI**操作 DevCon に更新するデバイス ドライバーが表示されないためです。

システムは、この変更を有効にするを再起動する必要があります。 DevCon システムを再起動するのには、再起動の条件付きパラメーターを追加します (/r) コマンド。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>サンプルの使用法

```
devcon updateni c:\windows\inf\newdvc.inf ISAPNP\CSC4324\0
devcon /r updateni c:\windows\inf\newdvc.inf *PNP030b
```

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

[例: 32:通信ポートのドライバーを更新します。](devcon-examples.md#ddk_example_32_update_the_driver_for_communication_ports_tools)









