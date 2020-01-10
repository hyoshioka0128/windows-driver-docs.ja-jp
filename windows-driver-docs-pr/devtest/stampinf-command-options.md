---
title: Stampinf コマンドのオプション
description: Stampinf は、共通の INF ファイルディレクティブを更新するコマンドラインツールです。
ms.assetid: 409b1bcc-9e19-4a95-a459-fc9f1ec41ea1
keywords:
- Stampinf コマンドオプションドライバー開発ツール
topic_type:
- apiref
api_name:
- Stampinf
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0bb394ca77654a333863aff92163b3d9a261633
ms.sourcegitcommit: b06bf47dca21779d4cbcaf43d7485815aa2a35fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/08/2020
ms.locfileid: "75737607"
---
# <a name="stampinf-command-options"></a>Stampinf コマンドのオプション


Stampinf は、共通の INF ファイルディレクティブを更新するコマンドラインツールです。

```
Stampinf -f filename 
[-s section] 
[-d [date | *]] 
[-a [architecture]] 
[-c catalogfile]
[-v [time | *]]
[-k version] 
[-u version]
[-i path]
[-n]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______-f________filename______"></span><span id="_______-F________FILENAME______"></span> **-f** *ファイル名*   
処理する INF ファイルまたは INX ファイルを指定します。

<span id="-s_section"></span><span id="-S_SECTION"></span> **-s** *セクション*  
[**INF DriverVer ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive)を追加する INF セクションを指定します。 このディレクティブの既定の場所は、[**INF Version セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)です。

<span id="_______-d_________date_____"></span><span id="_______-D_________DATE_____"></span> **-d** \[*日付* |  **\\** <em>\]  
[INF DriverVer ディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive)で記述される日付を指定します。 日付の形式は、月/日/年</em> ( **-d 10/20/2011**など) です。

現在の日付を使用するには、このパラメーターを使用してアスタリスク (\*) を指定します。

**-D**パラメーターを指定しなかった場合、またはオプションを指定せずに指定した場合、Stampinf では次のいずれかの日付値が使用されます。

-   STAMPINF\_DATE 環境変数が設定されている場合、Stampinf では、この環境変数によって指定された日付値が使用されます。

-   STAMPINF\_DATE 環境変数が指定されていない場合、Stampinf は現在の日付を使用します。

<span id="_______-a_________architecture______________"></span><span id="_______-A_________ARCHITECTURE______________"></span> **-\[** *アーキテクチャ* **\]**    
INX ファイルで使われている $ARCH$ 変数を置き換える "*アーキテクチャ*" 文字列を指定します。 $ARCH $ 変数は、 [**INF の製造元セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section)の**TargetOSVersion**装飾と、それぞれのセクション名を特定のプラットフォームにカスタマイズするために使用されます。 $ARCH $ 変数の詳細については、「 [USING INX files To CREATE INF files](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-inx-files-to-create-inf-files)」を参照してください。

*アーキテクチャ*文字列の値は、 **x86**、 **64** (Itanium ベースのプラットフォームの場合)、および**x64** (amd64 プラットフォームの場合) です。

**-A**パラメーターが指定されていない場合、またはオプションを指定せずに指定された場合、Stampinf は [ビルド環境] ウィンドウで設定されたプラットフォーム環境変数で指定された値を使用します。

<span id="_______-c________catalogfile______"></span><span id="_______-C________CATALOGFILE______"></span> **-c** *catalogfile*   
[**INF Version セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)の **CatalogFile** ディレクティブに書き込まれる値を指定します。 既定では、**CatalogFile** ディレクティブは書き込まれません。

<span id="_______-v_________time_____"></span><span id="_______-V_________TIME_____"></span> **-v \[** *time* **| \*\]**  
[**INF DriverVer ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive)に書き込まれるバージョン番号の時刻を指定します。 時刻の書式は *hours.minutes.seconds.milliseconds* です (例: 11.30.20.15)。 このオプションはドライバーのバージョン番号を増やす方法として便利であり、開発時に重宝します。

現在の時刻を使うには、このパラメーターと共にアスタリスク (\*) を指定します。

**-V**パラメーターが指定されていない場合、またはオプションを指定せずに指定された場合、Stampinf は次のバージョン番号の値のいずれかを使用します。

-   STAMPINF\_VERSION 環境変数が設定されている場合、Stampinf は、この環境変数によって指定されたバージョン番号の値を使用します。

-   STAMPINF\_VERSION 環境変数が指定されていない場合、Stampinf は Ntverp .h ファイルからバージョン番号を抽出します。

<span id="_______-k________version______"></span><span id="_______-K________VERSION______"></span> **-k** *バージョン*   
このドライバーが依存する KMDF の*バージョン*を指定します。 これは、INF ファイル内の KmdfLibraryVersion と KMDF 共同インストーラー名をカスタマイズするために使われます。 このオプションは、INF ファイル内の $KMDFVERSION$ キーワードと $KMDFCOINSTALLERVERSION$ キーワードを置き換えます。 この文字列の書式は次のようになります。

*メジャー\_バージョン&gt;を &lt;します。マイナー\_バージョンを&lt;&gt;*

たとえば、バージョン文字列として 1.5 を指定すると、1 つのキーワードに値 1.5 が使われ、もう 1 つのキーワードに 01005 が使われます。

<span id="_______-u________version______"></span><span id="_______-U________VERSION______"></span> **-u** *バージョン*   
このドライバーが依存する UMDF の*バージョン*を指定します。 このオプションは、INF ファイル内の UmdfLibraryVersion と UMDF 共同インストーラー名を指定するために使われます。 指定した*バージョン*は、INF ファイル内の $UMDFVERSION$ キーワードと $UMDFCOINSTALLERVERSION$ キーワードを置き換えます。 *バージョン*文字列の形式は次のとおりです。

*メジャー\_バージョン&gt;を&lt;* します。*マイナー\_バージョン&gt;を&lt;* します。 *&lt;サービス\_バージョン&gt;*

( *&lt;サービス\_バージョン&gt;* は通常 0) です。

たとえば、バージョン文字列として 1.5.0 を指定すると、メジャー キーワードに値 1.5.0 が使われ、マイナー キーワードに 01005 が使われます。

<span id="_______-n______"></span><span id="_______-N______"></span> **-n**   
詳細な Stampinf 出力を示します。

<span id="-i_path"></span><span id="-I_PATH"></span> **-i** *パス*  
Ntverp .h ファイルの場所を指定します。 *パス*は、Ntverp .h を含むディレクトリの完全修飾された場所を表します。

### <a name="comments"></a>備考

Stampinf が[**INF DriverVer ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive)に格納する日付値は、*協定世界時*(UTC) に基づいていません。これは*グリニッジ標準*時とも呼ばれます。 ただし、 [**Inf2Cat**](inf2cat.md)は、この INF ディレクティブの日付値を UTC 値として解釈します。 Stampinf によって使用されるローカル日付値が明日の日付の UTC 値として Inf2Cat によって解釈されると、エラーが発生する可能性があります。 この問題を回避するには、次の*いずれか*の操作を行います。

-   STAMPINF\_DATE 環境変数に、該当する UTC 日付値を設定します。 次**に、-d**パラメーターを指定せずに Stampinf を実行します。 これは、STAMPINF\_DATE 環境変数で指定された日付値を使用するように Stampinf に指示します。  Stampinf と Inf2Cat の両方で UTC が使用されるようになりました。
-   Inf2Cat が `/uselocaltime`に設定されるように、ドライバーパッケージのプロジェクト設定を変更します。 このためには、 **[構成プロパティ] -> [Inf2Cat] -> [全般] -> [Use Local Time]\(現地時刻の使用\)** を使用します。 Stampinf と Inf2Cat の両方で現地時刻が使用されるようになりました。

ドライバーを開発するときに、環境変数 PRIVATE\_DRIVER\_PACKAGE を設定できます。 この変数が設定されると、Stampinf は、コマンドラインの設定に関係なく、 [**INF DriverVer ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive)に使用される日付とバージョンを現在の日付と時刻に設定します。 また、Stampinf は**Catalogfile**ディレクティブを設定します。 Stampinf は、カタログが **-c**コマンドオプションで既に指定されていない限り、 [**INF バージョンセクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)に**catalogfile = delta. cat**を書き込みます。

ビルドウィンドウに次のコマンドを入力して、この開発モードを有効にします。

```
set PRIVATE_DRIVER_PACKAGE=1
```

 

 





