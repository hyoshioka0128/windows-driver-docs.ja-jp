---
title: 埋め込みの署名を使用したドライバーのリリース署名
description: 埋め込みの署名を使用したドライバーのリリース署名
ms.assetid: ffea2479-83ee-4d94-a5e6-73ecea9fc17d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3a5211765376f79d059820454d2f7747b3256a3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580056"
---
# <a name="release-signing-a-driver-through-an-embedded-signature"></a>埋め込みの署名を使用したドライバーのリリース署名


符号付き[カタログ ファイル](catalog-files.md)を正しくインストールして、ほとんどを読み込むことが必要、[ドライバー パッケージ](driver-packages.md)します。 ただし、埋め込まれた署名可能性がありますも選択肢になります。 カタログ ファイルにデジタル署名を保存せずに、ドライバーのバイナリ イメージ ファイル自体にデジタル署名を追加するには埋め込まれた署名です。 その結果、ドライバーが埋め込みで署名されたドライバーのバイナリ イメージが変更されます。

カーネル モード バイナリの埋め込まれた署名 (たとえば、ドライバーと関連付けられている .dll ファイル) に必要なときに。

-   ドライバーは、*ブート開始ドライバー*します。 Windows Vista および Windows での以降のバージョンの 64 ビット バージョンでは、[カーネル モード コード署名の要件](kernel-mode-code-signing-requirements--windows-vista-and-later-.md)状態を*ブート開始ドライバー*埋め込みの署名が必要です。 これは、ドライバーのドライバー パッケージがデジタル署名済みカタログ ファイルを持つかどうかに関係なく必要です。

-   カタログ ファイルが含まれていないドライバー パッケージをドライバーがインストールされます。

同様[カタログ ファイル](catalog-files.md)、 [ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)ツールを使用して、テスト証明書を使用してカーネル モード バイナリ ファイル内のデジタル署名を埋め込みます。 次のコマンドラインは、署名ツールは、次を実行する方法を示します。

-   テスト署名 Toastpkg サンプルの 64 ビット バージョンのバイナリ ファイル、toaster.sys します。 WDK のインストール ディレクトリ内でこのファイルにある、 *src\\全般\\トースター\\toastpkg\\toastcd\\amd64*ディレクトリ。

-   使用して、[ソフトウェア発行元証明書 (SPC)](software-publisher-certificate.md)商用証明書機関 (CA) によって発行されました。

-   SPC の互換性のある複数の証明書を使用します。

-   タイム スタンプ機関 (TSA) 経由のデジタル署名にタイムスタンプを割り当てます。

テスト署名、 *toaster.sys*ファイルを次のコマンドラインを実行します。

```cpp
Signtool sign /v /ac MSCV-VSClass3.cer /s MyPersonalStore /n contoso.com /t http://timestamp.verisign.com/scripts/timstamp.dll amd64\toaster.sys
```

各項目の意味は次のとおりです。

-   **サインオン**コマンドは、指定されたカーネル モード バイナリ ファイルに署名する署名ツールを構成します。 *amd64\\toaster.sys*します。

-   **/V**で SignTool の表示が正常に実行し、警告メッセージの詳細な操作を有効にします。

-   **/Ac**オプションは、クロス証明書を格納するファイルの名前を指定します (*MSCV VSClass3.cer*)、CA から取得します。 クロス証明書は、現在のディレクトリにない場合は、完全なパス名を使用します。

-   **/S**オプションを個人証明書ストアの名前を指定します (*MyPersonalStore)* SPC を格納しています。

-   **/N**オプションは、証明書の名前を指定します (*Contoso.com)* は指定された証明書ストアにインストールされています。

-   **/T**オプション、TSA の URL を指定します (*http://timestamp.verisign.com/scripts/timstamp.dll*) タイムスタンプをデジタル署名がこれです。

    **重要な**  キーの失効がコード署名の秘密キーの署名者の場合は、侵害の必要な情報を提供するタイムスタンプを含むです。

     

-   *amd64\\toaster.sys*埋め込まれた署名されるカーネル モード バイナリ ファイルの名前を指定します。

SignTool とコマンドライン引数の詳細については、次を参照してください。 [ **SignTool**](https://msdn.microsoft.com/library/windows/hardware/ff551778)します。

埋め込みの署名でのドライバーをリリース署名の詳細については、次を参照してください。[ドライバー パッケージのリリース署名](release-signing-driver-packages.md)と[ドライバー ファイルをリリース署名](release-signing-a-driver-file.md)します。

 

 





