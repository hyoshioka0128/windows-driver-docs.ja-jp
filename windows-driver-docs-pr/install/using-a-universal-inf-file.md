---
title: Using a Universal INF File (ユニバーサル INF ファイルの使用)
description: ユニバーサルまたはモバイルのドライバー パッケージを作成する場合は、ユニバーサル INF ファイルを使用する必要があります。
ms.assetid: 2CBEB814-974D-4E8B-A44A-2CFAA8D4C94E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5404dcfd2b5d342fafaf4122d8ae08108e30e2ef
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384775"
---
# <a name="using-a-universal-inf-file"></a>Using a Universal INF File (ユニバーサル INF ファイルの使用)

ユニバーサルまたはモバイルのドライバー パッケージを作成する場合は、ユニバーサル INF ファイルを使用する必要があります。 デスクトップのドライバー パッケージを作成する場合、ユニバーサル INF ファイルを使用する必要はありませんが、ため実行がパフォーマンス上の利点のため推奨は。

ユニバーサル INF ファイルのサブセットを使用して、 [INF 構文](inf-file-sections-and-directives.md)Windows ドライバーを使用します。 ユニバーサル INF ファイルは、ドライバーをインストールし、デバイスのハードウェアを構成しますが、共同インストーラーを実行するなど、他の任意の操作は実行されません。

## <a name="why-is-a-universal-inf-file-required-on-non-desktop-editions-of-windows"></a>Windows のデスクトップ以外のエディションで必要なユニバーサル INF ファイルはなぜですか。

Windows、Windows 10 Mobile などの一部のエディションは、ドライバーのインストールのプラグ アンド プレイのメカニズムをサポートしていません。 そのため、ドライバーのインストールには、ターゲット システムのオフライン イメージに対して行われます。 Microsoft Visual Studio では、このようなターゲット システム用にドライバーをビルド、すべてのレジストリ設定を適用するを含む XML ベースの構成ファイルを生成します。 その結果に INF ファイルは、このようなシステムは、システムの実行時の動作に依存しない加法操作のみを実行する必要があります。 このような制限付きの構文を使用して、INF ファイルには、ユニバーサル INF ファイルは呼び出されます。

ユニバーサル INF ファイルは、毎回同じ結果を予測的にインストールします。 インストールの結果は、システムの実行時の動作に依存しません。 たとえば、共同インストーラーの参照はオフラインのシステムで追加 DLL でのコードを実行できないため、ユニバーサル INF ファイルでは無効です。

その結果、ユニバーサル INF ファイルを使用してドライバー パッケージを事前に構成されているし、オフライン システムに追加します。

使用することができます、 [InfVerif](../devtest/infverif.md)ドライバーの INF ファイルに汎用場合をテストするためのツール。

## <a name="which-inf-sections-are-invalid-in-a-universal-inf-file"></a>INF セクションがユニバーサル INF ファイルでは無効です。

任意の INF セクションは、次を除くユニバーサル INF ファイルで使用できます。

-   [**INF ClassInstall32 セクション**](inf-classinstall32-section.md)
-   [**INF DDInstall.CoInstallers セクション**](inf-ddinstall-coinstallers-section.md)
-   [**INF DDInstall.FactDef Section**](inf-ddinstall-factdef-section.md)
-   [**INF DDInstall.LogConfigOverride Section**](inf-ddinstall-logconfigoverride-section.md)

[ **INF 製造元セクション**](inf-manufacturer-section.md)は有効な限り、 **TargetOSVersion**装飾が含まれていない、 **ProductType**フラグまたは**SuiteMask**フラグ。

## <a name="which-inf-directives-are-invalid-in-a-universal-inf-file"></a>どの INF ディレクティブがユニバーサル INF ファイルでは無効ですか。


任意の INF ディレクティブは、次を除くユニバーサル INF ファイルで使用できます。

-   [**INF BitReg ディレクティブ**](inf-bitreg-directive.md)
-   [**INF DelFiles ディレクティブ**](inf-delfiles-directive.md)
-   [**INF DelProperty ディレクティブ**](inf-delproperty-directive.md)
-   [**INF DelReg Directive**](inf-delreg-directive.md)
-   [**INF DelService ディレクティブ**](inf-delservice-directive.md)
-   [**INF Ini2Reg ディレクティブ**](inf-ini2reg-directive.md)
-   [**INF LogConfig ディレクティブ**](inf-logconfig-directive.md)
-   [**INF ProfileItems ディレクティブ**](inf-profileitems-directive.md)
-   [**INF RegisterDlls ディレクティブ**](inf-registerdlls-directive.md)
-   [**INF RenFiles ディレクティブ**](inf-renfiles-directive.md)
-   [**INF UnregisterDlls ディレクティブ**](inf-unregisterdlls-directive.md)
-   [**INF UpdateIniFields ディレクティブ**](inf-updateinifields-directive.md)
-   [**INF UpdateInis ディレクティブ**](inf-updateinis-directive.md)

次のディレクティブでは、いくつかの注意事項で有効です。

-   [ **INF AddReg ディレクティブ**](inf-addreg-directive.md)は有効な場合、指定したエントリ*追加レジストリ セクション*が、 *reg ルート*の値**HKR**、または、次の場合。
    -   登録の[コンポーネント オブジェクト モデル](https://docs.microsoft.com/windows/desktop/com)(COM) オブジェクト、キーは、書き込むことができます。
        -   HKCR
        -   Hklm \software\classes
    -   作成の[ハードウェア Media Foundation 変換](https://docs.microsoft.com/windows/desktop/medfound/media-foundation-transforms)(仕様) キーは、書き込むことができます。
        -   HKLM\SOFTWARE\Microsoft\Windows Media Foundation
        -   HKLM\SOFTWARE\WOW6432Node\Microsoft\Windows Media Foundation
        -   HKLM\SOFTWARE\WOW3232Node\Microsoft\Windows メディア ファンデーション

-   [**INF CopyFiles ディレクティブ**](inf-copyfiles-directive.md)は有効な場合にのみ、[先ディレクトリ](inf-destinationdirs-section.md)は、次のいずれか。

    -   11 (%windir% に対応する\\System32)
    -   12 (%windir% に対応する\\System32\\ドライバー)
    -   13 (%windir% の下のディレクトリに対応する\\System32\\DriverStore\\FileRepository ドライバーが格納されている)  
            **注:** CopyFiles は、対象のファイル名の変更は使用できません**DestinationDirs**が含まれています*dirid* 13。 また、 *dirid* 13 のみデバイス インストールのシナリオの限定されたサブセット用の Windows 10 製品に有効です。  詳細については、特定のデバイス クラスのガイダンスとサンプルを参照してください。
    -   10、SysWOW64 (%windir% に対応する\\SysWOW64)
    -   10、*ベンダー固有のサブディレクトリの名前*  
            **注:** Windows 10、バージョン 1709 を使用してで*dirid*ベンダー固有のサブディレクトリの名前を持つ 10 を使用する測定とユニバーサル INF で有効では、 [InfVerif](../devtest/infverif.md)ツール。  今後のリリースで、この値をサポートしない可能性があります。  移行をお勧めします。 *dirid* 13。

## <a name="see-also"></a>関連項目

* [ユニバーサル Windows ドライバーをインストールします。](https://docs.microsoft.com/windows-hardware/drivers)
* [InfVerif](https://docs.microsoft.com/windows-hardware/drivers/devtest/infverif)
