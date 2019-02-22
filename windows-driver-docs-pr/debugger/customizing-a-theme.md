---
title: テーマのカスタマイズ
description: テーマのカスタマイズ
ms.assetid: 3dddbf19-34ec-4cb0-b427-854ae7622fa1
keywords:
- テーマをカスタマイズします。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0bf54b37d4ac1e7941f83276a8744c93b8e7e15
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549581"
---
# <a name="customizing-a-theme"></a>テーマのカスタマイズ


## <span id="ddk_creating_and_opening_a_workspace_dbg"></span><span id="DDK_CREATING_AND_OPENING_A_WORKSPACE_DBG"></span>


テーマをカスタマイズする前にする必要があります最初に読み込むことができます。 参照してください[テーマの読み込み](loading-a-theme.md)詳細についてはします。

テーマが読み込まれた後は、コマンド ライン パラメーターのない WinDbg を開始します。 これは、基本のワークスペースを開きます。 テーマをカスタマイズするためのフォーカスの 2 つの一般的な領域がある: パスの設定と、ウィンドウの位置を調整します。

調整が WinDbg を終了し、選択して、ワークスペースを保存します。 必要に応じていずれかを行った後**ワークスペースの保存**から、**ファイル**メニュー。 Regedit を開き、新しい設定を .reg ファイルに保存する場合は、下のレジストリ キーをエクスポート**HKCU\\ソフトウェア\\Microsoft\\Windbg\\ワークスペース**.reg ファイル。

### <a name="span-idsettingpathsspanspan-idsettingpathsspansetting-paths"></a><span id="setting_paths"></span><span id="SETTING_PATHS"></span>パスの設定

適切なパスを設定するには、WinDbg が効果的にデバッグする必要があるファイルのすべてを検索できることを保証できます。 設定する 3 つのメイン パスがあります。 シンボル パス、ソース パス、および実行可能イメージのパス。

ここでは、シンボルとソースのパスを設定する方法の例を示します。 実行可能イメージのパスは、通常、シンボル パスとして同じです。

シンボル パスを設定するには。

```text
SRV*c:\MySymCache*\\CompanySymbolServer\Symbols;SRV*c:\WinSymCache*https://msdl.microsoft.com/download/symbols
```

ソース パスを設定するには。

```text
SRV*;d:\MySourceRoot
```

### <a name="span-idadjustingwindowpositionspanspan-idadjustingwindowpositionspanadjusting-window-position"></a><span id="adjusting_window_position"></span><span id="ADJUSTING_WINDOW_POSITION"></span>ウィンドウの位置を調整します。

テーマを使用する前に、WinDbg は、ソース ファイルを正しく処理できるようにウィンドウの配置を調整する必要があります。 これにより、ソース ウィンドウをドッキングする場所を知っていること。

WinDbg でソース ウィンドウを開くことから始めます。 タブとドッキング ウィンドウ、プレース ホルダーをソース ウィンドウ用に確保します。 適切な関係にするためには、プレース ホルダー ウィンドウはこのタブのドッキングの操作を実行する前に、ドッキング ステーションに最前面のウィンドウをある必要があります。 ソース ウィンドウがプレース ホルダーのウィンドウではないを閉じるようになりました。

デバッグ情報の windows「記憶」最後にドッキング操作、ため、この手順を実行した後各ソース ウィンドウの最後のドッキング操作はプレース ホルダーの windows のいずれかで関連付けられています。 このメモリ属性によりを閉じないでください、プレース ホルダーの windows のいずれか。 さらに、テーマの構成を変更する場合は、ドックの位置を変更する任意のウィンドウは常にプレース ホルダー ファイルとタブのドッキングします。

次の操作を使用して、デバッグ ツールの Windows に含まれているサンプルのテーマが作成されました。

プレース ホルダーの位置に置き\*ドッキング ステーションに .c ファイル。

タブのドッキングするプレース ホルダーの必要なウィンドウの上のすべてのウィンドウ型。

WinDbg のウィンドウの位置の調整に関する詳細については、次を参照してください。 [、Windows の位置づけ](positioning-the-windows.md)します。

 

 





