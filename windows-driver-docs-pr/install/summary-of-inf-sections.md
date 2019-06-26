---
title: INF セクションの概要
description: INF セクションの概要
ms.assetid: a9d4691b-4429-456b-a5d2-482ccd0a2845
keywords:
- INF ファイルのセクションでは、WDK のデバイス インストール
- WDK の INF ファイルのセクションでは
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa0b03aac3d3887d79b4db17c3a31762e4a25caa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385872"
---
# <a name="summary-of-inf-sections"></a>INF セクションの概要





INF ファイルで使用できるシステム定義のセクションを以下に示します。 システム定義のセクション名は大文字です。 たとえば、**バージョン**、**バージョン**、および**バージョン**INF ファイル内で有効なセクションの名前です。

このセクションでは、ほとんどのデバイスの INF ファイルで一般に出現する順序で、INF ファイルでセクションについて説明します。 ただし、これらのセクションでは実際に指定できます、任意の順序で。 Windows は、システム定義または INF ライター定義かどうか各 INF ファイル内のすべてのセクションをセクション名で、連続した順序ではなく検索します。

<a href="" id="version-section"></a>[**バージョン セクション**](inf-version-section.md)  
これは、INF ファイルごとに必要なセクションです。 Windows 2000 以降のバージョンの Windows でのインストールのこのセクションでは、有効な必要**署名**エントリ。

<a href="" id="signatureattributes-section"></a>[**SignatureAttributes セクション**](inf-signatureattributes-section.md)  
INF のこのセクションでは、一連のファイルに埋め込まれた、署名するハードウェア認定の一部として定義します。 これらの追加の署名は、特別なニーズの特定のデバイスの必要があります。 例については、保護された環境のメディアの再生、起動時マルウェア対策、およびサード パーティ製 HAL 拡張です。

<a href="" id="sourcedisksnames-section"></a>[**SourceDisksNames セクション**](inf-sourcedisksnames-section.md)  
このセクションは、INF ファイルに対応する場合に必要な**SourceDisksFiles**セクション。 IHV と OEM 提供のデバイスとそのドライバーをパッケージ化された製品に含まれる配布メディアからインストールするには、このセクションが必要です。 次のいずれかをインストールするこのような INF ファイルでも必要です。

- 共同インストーラー システム提供のデバイス クラスのインストーラーまたは共同インストーラーの操作を補足する DLL (も参照してください<em>DDInstall</em>**します。CoInstallers**この一覧の後半)

- 新しいクラスのインストーラー、OS のデバイスのインストーラーの操作を補足する DLL (も参照してください**ClassInstall32**)

このセクションでは、個々 のソース配布ディスクまたは、インストール CD-ROM のディスクを識別します。 これに対し、システムが指定した INF ファイルごとの指定、 **LayoutFile**内のエントリ、**バージョン**セクションし、ソース配布内容とレイアウトの詳細を示すその他の少なくとも 1 つの INF ファイルを提供すべてのソフトウェア コンポーネントをインストールします。

<a href="" id="sourcedisksfiles-section"></a>[**SourceDisksFiles セクション**](inf-sourcedisksfiles-section.md)  
このセクションでは、ターゲット コンピューターのバックアップ先に、配布メディアからインストールするファイルの場所を識別します。 このセクションのある INF ファイルが必要、 **SourceDisksNames**セクション。

<a href="" id="destinationdirs-section"></a>[**DestinationDirs セクション**](inf-destinationdirs-section.md)  
デバイスとドライバーの INF ファイルが、 **DestinationDirs**ファイルのコピーを INF 指定の既定のディレクトリを指定するセクションは、配布メディアにまたは INF のレイアウト ファイルに記載します。 INF ファイルで、一緒にインストールするのには、その INF 以外のファイルがない、モデムまたはディスプレイ モニターなどのデバイスにインストールしない場合、このセクションが必要です。

<a href="" id="controlflags-section"></a>[**ControlFlags セクション**](inf-controlflags-section.md)  
このセクションでは、配布メディアからファイルを転送にのみ、INF ファイルを使用するかどうかを制御します。

ほとんどの INF ファイルのデバイス ドライバーとシステム クラスのインストーラーがこのセクションのある一般的には、サブセットには少なくともを除外するように*モデル*をエンドユーザーに表示される、手動でインストール可能なデバイスの一覧からエントリ。 のみの PnP デバイスをインストールする INF ファイルでは、すべてのモデルに固有の情報を表示しないようにします。

<a href="" id="manufacturer-section"></a>[**製造元セクション**](inf-manufacturer-section.md)  
このセクションでは、デバイスとそのドライバーの INF ファイルに必要です。

**製造元**のシステム デバイス クラス INF セクションとも呼ばれます「の目次、」のエントリの各参照されて、INF-ライター定義*モデル*セクションで、これには、さらに、ごとのモデルのエントリをなど、追加の INF ライター定義セクションを参照して*DDInstall*セクション<em>DDInstall</em>**します。サービス**セクションなどです。

<a href="" id="models-section--per-manufacturer-entry--"></a>[**セクションをモデル化**](inf-models-section.md) (あたり**製造元**エントリ)   
このセクションでは INF ファイルがドライバーをインストールするデバイスを識別するために必要です。 一連のデバイスや、デバイス ID の名前の汎用名 (文字列) の間のマッピングを指定します、 *DDInstall*セクションで、デバイスのインストール手順を含む INF ファイルに別の場所。

1 つのプロバイダーの 1 つまたは複数のデバイスとドライバーをインストールする INF ファイルには、1 つだけを指定しなければ*モデル*セクションがのデバイス クラスに対するシステム INF ファイルは多くは INF ライター定義*モデル*セクション。

<a href="" id="ddinstall-section--per-models-entry--"></a>[ ***DDInstall*セクション**](inf-ddinstall-section.md) (あたり*モデル*エントリ)   
このセクションでは実際に記載されているすべてのデバイスをインストールするために必要な*モデル*と共にこのような各デバイスのドライバーの INF ファイルでセクション。 A *DDInstall*セクションは、1 つ以上で共有できる*モデル*セクション。

<a href="" id="ddinstall-services-section"></a>[***DDInstall *。「サービス」セクション**](inf-ddinstall-services-section.md)  
Microsoft Windows 2000 以降、このセクションは必須の拡張として、 *DDInstall*ほとんどのカーネル モード デバイス ドライバーのセクション。 これには、(例外は、モデムとディスプレイ モニターの INF ファイルを)、WDM ドライバーが含まれます。 特定のドライバーのサービスの開始方法とタイミングを制御、レガシなどを基になるへの依存性 (存在する場合)。 このセクションもセットアップ イベント ログ サービス デバイス ドライバーによってイベントのログ記録をサポートしている場合。

<a href="" id="ddinstall-hw-section"></a>[***DDInstall *。ハードウェア セクション**](inf-ddinstall-hw-section.md)  
この省略可能なセクションが特定のデバイスを追加します (通常、ドライバーに依存しない) 情報をレジストリまたは場合によって多機能デバイスか、または 1 つまたは複数の PnP フィルター ドライバーをインストールする、レジストリからこのような情報を削除します。

<a href="" id="ddinstall-coinstallers-section"></a>[***DDInstall *。CoInstallers セクション**](inf-ddinstall-coinstallers-section.md)  
**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このセクションが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

このオプションのセクションでは、1 つまたは複数デバイス固有 co-installer 配布メディアに、システムのデバイスのインストーラーのまたは既存のデバイス クラスのインストーラーの操作を補足する登録します。

共同インストーラーがする通常のレジストリに追加の構成情報を書き込むか場合は使用できませんを動的に生成される、マシン固有の情報を必要とするその他のインストール タスクを実行する IHV と OEM が提供 Win32 の DLL をデバイスの INF ファイルが作成されます。 詳細については、次を参照してください。[共同インストーラーの作成](writing-a-co-installer.md)です。

<a href="" id="ddinstall-factdef-section"></a>[***DDInstall *。FactDef セクション**](inf-ddinstall-factdef-section.md)  
**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このセクションが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

このセクションは、手動でインストールされている非 PnP デバイスの INF ファイルに含める必要があります。 工場出荷時既定ハードウェアの構成など、設定、バス相対 I/O ポート IRQ (ある場合)、やなど、カードのことを指定します。

<a href="" id="ddinstall-logconfigoverride-section"></a>[***DDInstall *。LogConfigOverride セクション**](inf-ddinstall-logconfigoverride-section.md)  
**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このセクションが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

このセクションの作成に使用されます、[構成をオーバーライドする](https://docs.microsoft.com/windows-hardware/drivers/kernel/hardware-resources#logical-configuration-types-for-resource-requirements-lists)、バス ドライバーのプラグ アンド プレイ デバイスの報告されたハードウェア リソース要件をオーバーライドします。

<a href="" id="ddinstall-interfaces-section"></a>[***DDInstall *。インターフェイス セクション**](inf-ddinstall-interfaces-section.md)  
ドライバーはカーネル ストリーミング静止画キャプチャまたはデータの圧縮解除などのインターフェイス クラスの新しいインスタンスを作成するため、デバイスのインターフェイス クラスの機能をエクスポートする場合、INF ファイルはこのセクションを持つことができます。

<a href="" id="interfaceinstall32-section"></a>[**InterfaceInstall32 セクション**](inf-interfaceinstall32-section.md)  
新しいクラス ドライバーなど、インストールするコンポーネントには、新しいする 1 つまたは複数が提供する場合[デバイス インターフェイス クラス](device-interface-classes.md)INF ファイルのこのセクションが、上位レベルのコンポーネントにします。 実際には、このセクションでは、インターフェイス クラスを提供する機能を使用するために必要なものを設定して、一連の新しいクラスのデバイスのインターフェイスをブートス トラップします。

<a href="" id="defaultinstall-section"></a>[**DefaultInstall セクション**](inf-defaultinstall-section.md)  
INF ファイルの**DefaultInstall** INF ファイル名を右クリックして、"Install"メニュー項目を選択した場合、セクションにアクセスします。

<a href="" id="defaultinstall-services-section"></a>[**DefaultInstall.Services セクション**](inf-defaultinstall-services-section.md)  
このセクションと同じ、 [ **INF DDInstall.Services セクション**](inf-ddinstall-services-section.md)との関連付けで使用して、 [ **INF DefaultInstall セクション**](inf-defaultinstall-section.md).

<a href="" id="strings-section"></a>[**文字列のセクション**](inf-strings-section.md)  
このセクションでは、すべての INF ファイルでそれぞれを定義する必要が **%** <em>strkey</em> **%** INF で指定したトークン。 慣例により、**文字列**セクション (セクション、INF ロケール固有のセットを提供する場合または**文字列**のセクションでは) すべての保守とローカライズ性の INF ファイルをシステム提供の最後に表示されます。

いくつかのセクションにはここに示した特に*インストール*名前の INF ライター定義の追加のセクションを参照するディレクティブを含めることができます。 各ディレクティブには、インストール プロセス中に適切な種類 INF ライター定義のセクションの下に表示する項目で実行する特定の操作が発生します。

有効なエントリと前の一覧に、特定のセクションのディレクティブのセットは、特定のセクション オブジェクトとこれらのセクションの各参照の正式な構文に示すです。 さらに、表示[INF ディレクティブの概要](summary-of-inf-directives.md)一般的に、ほとんどの概要は、ディレクティブを使用します。

オプションのエントリとそのような各セクション内でのディレクティブを次の例と、太字でない角かっこで囲まれています。

**\[バージョン\]** .\[**プロバイダー = %** <em>INF 作成者</em> **%** \] .**プロバイダー**内のエントリを **\[バージョン\]** セクションはすべての INF ファイルで必須のエントリではないことの意味では省略可能です。

 

 





