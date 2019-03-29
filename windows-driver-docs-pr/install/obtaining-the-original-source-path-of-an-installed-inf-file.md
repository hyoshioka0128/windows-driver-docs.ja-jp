---
title: インストール済みの INF ファイルの元のソース パスの取得
description: インストール済みの INF ファイルの元のソース パスの取得
ms.assetid: 7e086248-b11d-43ee-9afa-fad6f2136dc8
keywords:
- SetupAPI 関数 WDK、INF ファイル
- WDK SetupAPI のパス
- INF ファイル WDK SetupAPI
- WDK の INF ファイルのソース パス
- 元のソース パス WDK INF ファイル
- INF ファイルのパス情報を取得します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9091d8630a507d9f92ac3f759adc08570397a5e1
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349732"
---
# <a name="obtaining-the-original-source-path-of-an-installed-inf-file"></a>インストール済みの INF ファイルの元のソース パスの取得


このトピックでは、システムの INF ディレクトリにインストールされている INF ファイルの元のソース パスを取得する方法について説明します。 ない[SetupAPI](setupapi.md)この検索を直接実行する関数を実行できましていない取得直接を取得する INF ファイルのエントリにアクセスする SetupAPI 関数を使用できるように、INF ファイルにエントリを含めることによってインストール済みの INF ファイルから元のソース パス情報。

このメソッドは、システムの INF ファイルのディレクトリにインストールされている INF ファイルに対してのみ機能します。 このメソッドを使用して INF ファイルに存在することはできません、[ドライバー ストア](driver-store.md)します。

トースター サンプル Windows Driver Kit (WDK) で提供される共同インストーラーはこのメソッドを使用して、このトピックでは、このメソッドを示すトースター サンプルから抜粋します。 トースター サンプルの詳細については、次を参照してください。 *toasterpkg.htm*、に表示されている、 *src\\全般\\トースター* WDK のディレクトリ。

このメソッドを使用して、インストール済みの INF ファイルの元のソース パスを取得する、次の操作を行います。

1.  最初のフィールドが 1% 文字列キー トークンは、エントリを含むセクションには INF ファイルが含まれます。 既定では、1% 文字列キー トークンは、INF ファイルの元のソース パスを表します。 Windows では、このような INF ファイルがインストールされ、INF ファイルのバージョンと元のソース パス文字列が保存されます。 この例で示すように、%1% が使用されている場合に、このメソッドをのみ機能するを認識します。 一般に、どのような %1% が解決されるとはコンテキストによって異なります。 1% フィールドなど、*追加レジストリ セクション*エントリは、元のソース パスに解決されません。 このコンテキストで %1% が内の対応する INF ファイルのパスに解決される代わりに、[ドライバー ストア](driver-store.md)します。

2.  使用**SetupOpenInfFile**、 **SetupFindFirstLine**、および**SetupGetStringField** % 1% 文字列キー トークンを含むエントリから元のソース パスを取得します。

たとえば、 *toasterpkg.inf*次が含まれています\[ToasterCoInfo\]セクションで、カスタム OriginalInfSourcePath エントリを持つ最初のフィールドが 1% 文字列キー トークン。

```cpp
[ToastCoInfo]
; Used by the toaster co-installer to figure out where the original media is
; located (so it can start value-added setup programs).
OriginalInfSourcePath = %1%
```

トースター サンプルで示すように、INF を構成する場合、システムの INF ディレクトリの INF ファイルをインストールした後、元のソース パスを取得できます。 元のソース パス、最初の呼び出しを取得する**SetupOpenInfFile**インストールされている INF ファイルを開きます。 次のコード例から、 *toastco.c*開き、インストールされている*toasterpkg.inf*ファイル。

```cpp
// Since the INF is already in %SystemRoot%\Inf, we need to find out where it
// originally came from.  There is no direct way to ascertain an INF's
// path of origin, but we can indirectly determine it by retrieving a field
// from our INF that uses a string substitution of %1% (DIRID_SRCPATH).
//
hInf = SetupOpenInfFile(DriverInfoDetailData->InfFileName,
                        NULL,
                        INF_STYLE_WIN4,
                        NULL
                        );
```

インストール済みの INF ファイルを開いたら、呼び出す**SetupFindFirstLine**エントリを持つ最初のフィールドが 1% 文字列キー トークンを格納するセクションの最初の行を取得します。 次に、呼び出す**SetupGetStringField**にこのエントリの最初のフィールドを取得し、INF ファイルの元のソース パスを取得します。 次のコード例から、 *toastco.c*をカスタム OriginalInfSourcePath エントリを含み、このエントリの最初のフィールドを取得し、行を取得します。 元の INF の最初のフィールドが 1% 文字列キー トークンであるため**SetupGetStringField** INF ファイルの元のソース パスを返します。

```cpp
// Contained within our INF should be a [ToastCoInfo] section with the
// following entry:
//
//     OriginalInfSourcePath = %1%
//
// If we retrieve the value (i.e., field 1) of this line, we'll get the
// full path where the INF originally came from.
//
if(!SetupFindFirstLine(hInf, L"ToastCoInfo", L"OriginalInfSourcePath", &InfContext)) {
   goto clean0;
}
if(!SetupGetStringField(&InfContext, 1, *MediaRootDirectory, MAX_PATH, &PathLength) ||
  (PathLength <= 1)) {
  goto clean0;
```

 

 





