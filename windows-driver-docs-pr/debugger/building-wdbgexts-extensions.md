---
title: WdbgExts 拡張機能の作成
description: WdbgExts 拡張機能の作成
ms.assetid: a3923de6-bed5-40e0-a9cb-99e0f4354448
keywords:
- ビルド ユーティリティ (build.exe) WdbgExts 拡張機能の作成
- WdbgExts 拡張機能の構築
- コンパイル、WdbgExts 拡張機能
ms.date: 10/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: d76e961f07cb4cedab340efcfd8b0f82d96c3527
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530587"
---
# <a name="building-wdbgexts-extensions"></a>WdbgExts 拡張機能の作成


## <span id="ddk_building_wdbgexts_extensions_dbwx"></span><span id="DDK_BUILDING_WDBGEXTS_EXTENSIONS_DBWX"></span>


すべてのデバッガー拡張機能はコンパイルされ、ビルド ユーティリティを使用して構築する必要があります。 ビルド ユーティリティは、Windows Driver Kit (WDK) で、以前のバージョンの Windows DDK に含まれています。

次の点に注意してください。

-  WDK には、いくつかの別のビルド環境ウィンドウがあります。 対応するショートカットがこれらの各、**開始**メニュー、WDK をインストールするとします。 デバッガー拡張機能をビルドするには、拡張機能で実行して、どのようなプラットフォームに関係なく、最新の Windows ビルド環境を使用する必要があります。

-  ビルド ユーティリティは、通常は空白が含まれるディレクトリ パスにあるコードをコンパイルすることができません。 拡張機能のコードは、完全なパスにスペースが含まれていない、ディレクトリに配置する必要があります。 (具体的には、つまり、Program Files - 既定の場所にツールを Windows のデバッグをインストールする場合\\--Windows のツールをデバッグ サンプル拡張機能を構築することはできません)。

**デバッガーの拡張機能を構築するには**

1. 最新の Windows ビルド環境ウィンドウを開きます。 (「無料」のバージョンまたは「チェックを行う」のバージョンのいずれかを選択することができます - 配置した場合を除き、同一の結果が返って **\#ifdef DBG**ステートメントをコードにします)。

2. 変数を設定\_NT\_ターゲット\_バージョンを拡張機能を実行する Windows の最も古いバージョンを示します。 \_NT\_ターゲット\_バージョンは、次の値に設定することができます。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">Value</th>
    <th align="left">Windows のバージョン</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>_NT_TARGET_VERSION_WIN2K</p></td>
    <td align="left"><p>Windows 2000 以降。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>_NT_TARGET_VERSION_WINXP</p></td>
    <td align="left"><p>Windows XP 以降。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>_NT_TARGET_VERSION_WS03</p></td>
    <td align="left"><p>Windows Server 2003 以降。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>_NT_TARGET_VERSION_LONGHORN</p></td>
    <td align="left"><p>Windows Vista 以降。</p></td>
    </tr>
    </tbody>
    </table>

     

 場合\_NT\_ターゲット\_バージョンが設定されていない、拡張機能の Windows のバージョンでのみ実行ビルド ウィンドウが開かれた (およびそれ以降のバージョン)。 たとえば、ソース ファイルで、次の行を配置することと、Windows 上で実行される拡張機能がビルドされます。
    ```console
    _NT_TARGET_VERSION = $(_NT_TARGET_VERSION_WINXP) 
    ```

3. 設定、DBGSDK\_INC\_パスと DBGSDK\_LIB\_デバッガー SDK のヘッダーと、デバッガーの SDK ライブラリへのパスをそれぞれ指定するパス環境変数。 場合 *% デバッガー*ルートを表す、Windows のツールをデバッグ インストールのこれらの変数を次のように設定する必要があります。

    ```console
    set DBGSDK_INC_PATH=%debuggers%\sdk\inc
    set DBGSDK_LIB_PATH=%debuggers%\sdk\lib
    ```

    別の場所にこれらのヘッダーとライブラリを移動した場合は、その場所を指定します。

4. 拡張機能のディレクトリのファイルまたはソース ファイルが含まれているディレクトリには、現在のディレクトリを変更します。

5. ビルド ユーティリティを実行します。

    ```console
    build -cZMg
    ```

詳細については、これらの手順と、ディレクトリのファイルとソース ファイルを作成する方法の説明については、WDK のビルド ユーティリティのドキュメントを参照してください。

 

 





