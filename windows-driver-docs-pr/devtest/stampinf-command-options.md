---
title: Stampinf コマンドのオプション
description: Stampinf は、共通の INF ファイルのディレクティブを更新するコマンド ライン ツールです。
ms.assetid: 409b1bcc-9e19-4a95-a459-fc9f1ec41ea1
keywords:
- Stampinf コマンド オプションのドライバーの開発ツール
topic_type:
- apiref
api_name:
- Stampinf
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6e0df9663746f1d1555ba23e5b59d35fb188907
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387911"
---
# <a name="stampinf-command-options"></a>Stampinf コマンドのオプション


Stampinf は、共通の INF ファイルのディレクティブを更新するコマンド ライン ツールです。

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

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-f________filename______"></span><span id="_______-F________FILENAME______"></span> **-f** *filename*   
処理するための INF または INX ファイルを指定します。

<span id="-s_section"></span><span id="-S_SECTION"></span>**-s** *section*  
[**INF DriverVer ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff547394)を追加する INF セクションを指定します。 このディレクティブの既定の場所は、[**INF Version セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547502)です。

<span id="_______-d_________date_____"></span><span id="_______-D_________DATE_____"></span> **-d** \[ *日付* | **\\**<em>\]  
記述された日付を指定します、 [ </em> *INF DriverVer ディレクティブ*<em>](<https://msdn.microsoft.com/library/windows/hardware/ff547394>)します。日付の形式は*月</em>/* 日付*/* 年 * (たとえば、 **-d 2011 年 10 月 20 日**)。

現在の日付を使用するには、アスタリスクを指定 (\*) このパラメーターを使用します。

場合、 **-d**パラメーターが指定されていないまたは Stampinf は次の日付値のいずれかを使用して、オプションを指定せず指定します。

-   場合、STAMPINF\_日付環境変数が設定されている、Stampinf はこの環境変数で指定された日付値を使用します。

-   場合、STAMPINF\_環境変数の日付が指定されていない、Stampinf が現在の日付を使用します。

<span id="_______-a_________architecture______________"></span><span id="_______-A_________ARCHITECTURE______________"></span> **-a \[** *architecture* **\]**   
INX ファイルで使われている $ARCH$ 変数を置き換える "*アーキテクチャ*" 文字列を指定します。 $ARCH$ 変数の使用をカスタマイズする、 **TargetOSVersion**で装飾、 [ **INF 製造元セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547454)と、特定のプラットフォームをそれぞれのセクション名。 $ARCH$ 変数の詳細については、次を参照してください。 [INX INF ファイルを作成するファイルを使用する](https://msdn.microsoft.com/library/windows/hardware/ff545473)します。

値、*アーキテクチャ*文字列は**x86**、 **64** (Itanium ベースのプラットフォーム用)、および**x64** (amd64 プラットフォーム) のです。

場合、 **-** パラメーターが指定されていないまたは Stampinf、ビルド環境ウィンドウに設定されているプラットフォーム環境変数で指定されている値を使用して、オプションを指定せず指定します。

<span id="_______-c________catalogfile______"></span><span id="_______-C________CATALOGFILE______"></span> **-c** *catalogfile*   
[**INF Version セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547502)の **CatalogFile** ディレクティブに書き込まれる値を指定します。 既定では、**CatalogFile** ディレクティブは書き込まれません。

<span id="_______-v_________time_____"></span><span id="_______-V_________TIME_____"></span> **-v \[** *time* **| \*\]**  
[**INF DriverVer ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff547394)に書き込まれるバージョン番号の時刻を指定します。 時刻の書式は *hours.minutes.seconds.milliseconds* です (例: 11.30.20.15)。 このオプションはドライバーのバージョン番号を増やす方法として便利であり、開発時に重宝します。

現在の時刻を使うには、このパラメーターと共にアスタリスク (\*) を指定します。

場合、 **-v**パラメーターが指定されていないまたは Stampinf は次のバージョン番号の値のいずれかを使用して、オプションを指定せず指定します。

-   場合、STAMPINF\_バージョン環境変数が設定されている、Stampinf はこの環境変数で指定されているバージョン番号の値を使用します。

-   場合、STAMPINF\_バージョン環境変数が指定されていない、Stampinf Ntverp.hNtverp.h ファイルからバージョン番号を抽出します。

<span id="_______-k________version______"></span><span id="_______-K________VERSION______"></span> **-k** *version*   
指定します、*バージョン*KMDF ドライバーが依存しているのです。 これは、INF ファイル内の KmdfLibraryVersion と KMDF 共同インストーラー名をカスタマイズするために使われます。 このオプションは、INF ファイル内の $KMDFVERSION$ キーワードと $KMDFCOINSTALLERVERSION$ キーワードを置き換えます。 この文字列の書式は次のようになります。

*&lt;主要な\_バージョン&gt;.&lt;マイナー\_バージョン&gt;*

たとえば、バージョン文字列として 1.5 を指定すると、1 つのキーワードに値 1.5 が使われ、もう 1 つのキーワードに 01005 が使われます。

<span id="_______-u________version______"></span><span id="_______-U________VERSION______"></span> **-u** *バージョン*   
このドライバーが依存する UMDF の*バージョン*を指定します。 このオプションは、INF ファイル内の UmdfLibraryVersion と UMDF 共同インストーラー名を指定するために使われます。 指定した*バージョン*は、INF ファイル内の $UMDFVERSION$ キーワードと $UMDFCOINSTALLERVERSION$ キーワードを置き換えます。 *バージョン*文字列には、次の形式します。

*&lt;主要な\_バージョン&gt;*.*&lt;マイナー\_バージョン&gt;*.*&lt;サービス\_バージョン&gt;*

(場所*&lt;サービス\_バージョン&gt;* は通常 0 です)。

たとえば、バージョン文字列として 1.5.0 を指定すると、メジャー キーワードに値 1.5.0 が使われ、マイナー キーワードに 01005 が使われます。

<span id="_______-n______"></span><span id="_______-N______"></span> **-n**   
詳細な Stampinf 出力を示します。

<span id="-i_path"></span><span id="-I_PATH"></span>**-i** *パス*  
Ntverp.h ファイルの場所を指定します。 *パス*Ntverp.h を格納するディレクトリの完全修飾の場所を表します。

### <a name="comments"></a>コメント

日付の値に Stampinf が格納された、 [ **INF DriverVer ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff547394)に基づいていない*世界協定時刻*(UTC) であるとも呼ばれます*グリニッジ標準時*します。 ただし、 [ **Inf2Cat** ](inf2cat.md) UTC 値としてこの INF ディレクティブの日付の値を解釈します。 これがエラーが発生する場合は明日の日付を UTC 値として、Stampinf によって使用されるローカルの日付の値が Inf2Cat によって解釈されます。 この問題を回避するには*1 つ*します。

-   設定、STAMPINF\_適切な UTC 日付の値を環境変数の日付。 Stampinf を指定せずに実行される、 **-d**パラメーター。 これにより、STAMPINF で指定された日付値を使用する Stampinf\_環境変数の日付。  今すぐ Stampinf と Inf2Cat の両方は、UTC を使用します。
-   Inf2Cat を設定するために、ドライバー パッケージのプロジェクトの設定を変更`/uselocaltime`します。 このためには、**[構成プロパティ] -> [Inf2Cat] -> [全般] -> [Use Local Time]\(現地時刻の使用\)** を使用します。 今すぐ Stampinf と Inf2Cat の両方は、ローカル時刻を使用します。

ドライバーを開発する際に、プライベート環境変数を設定することができます\_ドライバー\_パッケージ。 Stampinf 設定日時に使用されるバージョンでこの変数が設定されている場合、 [ **INF DriverVer ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff547394)現在の日付と時間、コマンドラインの設定に関係なく。 さらに、Stampinf 設定、 **CatalogFile**ディレクティブ。 Stampinf 書き込みます**CatalogFile=delta.cat**で、 [ **INF バージョン セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547502)でカタログが既に指定されていない場合、 **-c**コマンド オプション。

この開発モードを有効にするビルドのウィンドウで、次のコマンドを入力します。

```
set PRIVATE_DRIVER_PACKAGE=1
```

 

 





