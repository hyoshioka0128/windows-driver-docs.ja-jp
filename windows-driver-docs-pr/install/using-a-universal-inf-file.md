---
title: ユニバーサル INF ファイルの使用
description: ユニバーサルまたはモバイルのドライバーパッケージを作成する場合は、ユニバーサル INF ファイルを使用する必要があります。
ms.assetid: 2CBEB814-974D-4E8B-A44A-2CFAA8D4C94E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 517479adc9d31562812a27e2555839c2c55435e0
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242993"
---
# <a name="using-a-universal-inf-file"></a>ユニバーサル INF ファイルの使用

ユニバーサルまたはモバイルのドライバーパッケージを作成する場合は、ユニバーサル INF ファイルを使用する必要があります。 デスクトップドライバーパッケージを作成する場合は、ユニバーサル INF ファイルを使用する必要はありませんが、パフォーマンス上の利点があるため、この方法をお勧めします。

ユニバーサル INF ファイルでは、Windows ドライバーで使用できる[inf 構文](inf-file-sections-and-directives.md)のサブセットを使用します。 ユニバーサル INF ファイルは、ドライバーをインストールし、デバイスハードウェアを構成しますが、他の操作 (共同インストーラーの実行など) を実行しません。

## <a name="why-is-a-universal-inf-file-required-on-non-desktop-editions-of-windows"></a>Windows のデスクトップ以外のエディションではユニバーサル INF ファイルが必要なのはなぜですか。

Windows 10 Mobile など、Windows の一部のエディションでは、ドライバーのインストールにプラグアンドプレイメカニズムがサポートされていません。 そのため、ドライバーのインストールは、ターゲットシステムのオフラインイメージで実行されます。 Microsoft Visual Studio は、このようなターゲットシステムのドライバーをビルドするときに、適用されるすべてのレジストリ設定を含む XML ベースの構成ファイルを生成します。 そのため、このようなシステムの INF ファイルでは、システムの実行時の動作に依存しない加法操作のみを実行する必要があります。 このような制限された構文を含む INF ファイルは、universal INF ファイルと呼ばれます。

ユニバーサル INF ファイルは、毎回同じ結果を使用して、予想どおりにインストールされます。 インストールの結果は、システムの実行時の動作に依存しません。 たとえば、追加の DLL 内のコードはオフラインシステムで実行できないため、ユニバーサル INF ファイルでは、共同インストーラー参照は無効です。

その結果、ユニバーサル INF ファイルを使用したドライバーパッケージを事前に構成して、オフラインシステムに追加することができます。

[InfVerif](../devtest/infverif.md)ツールを使用すると、ドライバーの INF ファイルが universal であるかどうかをテストできます。

## <a name="which-inf-sections-are-invalid-in-a-universal-inf-file"></a>ユニバーサル INF ファイルでは、どの INF セクションも無効ですか。

次の場合を除き、ユニバーサル INF ファイルでは任意の INF セクションを使用できます。

-   [**INF ClassInstall32 セクション**](inf-classinstall32-section.md)
-   [**INF DDInstall. CoInstallers セクション**](inf-ddinstall-coinstallers-section.md)
-   [**INF DDInstall. FactDef セクション**](inf-ddinstall-factdef-section.md)
-   [**INF DDInstall. LogConfigOverride セクション**](inf-ddinstall-logconfigoverride-section.md)

**TargetOSVersion**デコレーションに**ProductType**フラグまたは**suitemask**フラグが含まれていない限り、 [**INF の製造元セクション**](inf-manufacturer-section.md)は有効です。

## <a name="which-inf-directives-are-invalid-in-a-universal-inf-file"></a>ユニバーサル INF ファイルでは、どの INF ディレクティブも無効ですか。


次の場合を除き、ユニバーサル INF ファイルでは任意の INF ディレクティブを使用できます。

-   [**INF BitReg ディレクティブ**](inf-bitreg-directive.md)
-   [**INF DelFiles ディレクティブ**](inf-delfiles-directive.md)
-   [**INF DelProperty ディレクティブ**](inf-delproperty-directive.md)
-   [**INF DelReg ディレクティブ**](inf-delreg-directive.md)
-   [**INF DelService ディレクティブ**](inf-delservice-directive.md)
-   [**INF Ini2Reg ディレクティブ**](inf-ini2reg-directive.md)
-   [**INF LogConfig ディレクティブ**](inf-logconfig-directive.md)
-   [**INF ProfileItems ディレクティブ**](inf-profileitems-directive.md)
-   [**INF RegisterDlls ディレクティブ**](inf-registerdlls-directive.md)
-   [**INF RenFiles ディレクティブ**](inf-renfiles-directive.md)
-   [**INF UnregisterDlls ディレクティブ**](inf-unregisterdlls-directive.md)
-   [**INF UpdateIniFields ディレクティブ**](inf-updateinifields-directive.md)
-   [**INF UpdateInis ディレクティブ**](inf-updateinis-directive.md)

次のディレクティブは、いくつかの注意事項があります。

-   [**INF AddReg ディレクティブ**](inf-addreg-directive.md)は、指定された*レジストリセクション*のエントリに**hkr**の*reg ルート*値がある場合、または次の場合に有効です。
    -   [コンポーネントオブジェクトモデル](https://docs.microsoft.com/windows/desktop/com)(COM) オブジェクトの登録の場合、キーは次のように記述できます。
        -   HKCR
        -   HKLM\SOFTWARE\Classes
    -   [ハードウェアメディアファンデーション変換](https://docs.microsoft.com/windows/desktop/medfound/media-foundation-transforms)(mfts) を作成する場合、キーは次のように記述できます。
        -   HKLM\SOFTWARE\Microsoft\Windows メディアファンデーション
        -   HKLM\SOFTWARE\WOW6432Node\Microsoft\Windows メディアファンデーション
        -   HKLM\SOFTWARE\WOW3232Node\Microsoft\Windows メディアファンデーション

-   [**INF CopyFiles ディレクティブ**](inf-copyfiles-directive.md)は、[コピー先のディレクトリ](inf-destinationdirs-section.md)が次のいずれかの場合にのみ有効です。

    -   11 (% WINDIR%\\System32) に対応
    -   12 (% WINDIR%\\System32\\ドライバー) に対応
    -   13 (ドライバーが格納されている% WINDIR%\\System32\\DriverStore\\FileRepository の下のディレクトリに対応)  
            **注:** CopyFiles は、 **Destinationdirs**に*dirid* 13 が含まれているファイルの名前を変更するために使用することはできません。 また、 *dirid* 13 は、デバイスのインストールシナリオの限られたサブセットについてのみ、Windows 10 製品で有効です。  詳細については、特定のデバイスクラスのガイダンスとサンプルを参照してください。
    -   10、SysWOW64 (% WINDIR%\\SysWOW64 に対応)
    -   10、*ベンダー固有のサブディレクトリ名*  
            **注:** Windows 10 バージョン1709では、ベンダー固有のサブディレクトリ名で*dirid* 10 を使用することは、 [InfVerif](../devtest/infverif.md)ツールを使用して測定されたユニバーサル INF で有効です。  今後のリリースでは、この値はサポートされない可能性があります。  *Dirid* 13 に移行することをお勧めします。

## <a name="see-also"></a>参照

* [ユニバーサル Windows ドライバーの概要](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)
* [InfVerif](https://docs.microsoft.com/windows-hardware/drivers/devtest/infverif)
