---
title: ローカライズされた MOF ファイルのビルドと展開
description: ローカライズされた MOF ファイルのビルドと展開
ms.assetid: 3a741dc6-a789-44e1-9d68-cdb41b7161ed
keywords:
- MOF ファイルの WDK WMI
- MOF ファイルをローカライズします。
- MUI バージョン WDK WMI
- マスターの MOF ファイルの WDK WMI
- WDK の WMI の言語
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 215b9ae3d09a1b4d96297d4a51a0029d12d91716
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338613"
---
# <a name="building-and-deploying-the-localized-mof-file"></a>ローカライズされた MOF ファイルのビルドと展開





Windows XP の各国語バージョンと以降のバージョンのオペレーティング システムは、2 つの選択肢は、単一言語 (ローカライズされた) バージョン、および多言語ユーザー インターフェイス (MUI) のバージョン。 Windows 版は MUI では、同時に複数の言語をサポートできます。

Windows のローカライズされたバージョンに展開されるドライバーには、すべてのクラスだけでなく、ローカライズされた言語の修正契約書および米国英語の言語の修正の言語に依存しないバージョンを含む MOF リソースを含める必要があります。

MUI のバージョンの Windows には、ドライバー イメージ自体は言語に依存しないと、WMI クラスの米国英語バージョンを含める必要があります。 %Windir% でサポートされている各追加言語のリソースのみのイメージを配置できる\\system32\\ドライバー\\MUI\\*langid*ディレクトリ場所*langid*の LCID は、ロケールにします。

必要に応じて、ドライバー イメージ自体は、サポートされているすべての言語を含めることができます。

言語がこれらのメカニズムのいずれかによってサポートされていない場合は、英語版が使用されます。

### <a name="building-distinct-mof-files-for-each-language"></a>言語ごとに個別の MOF ファイルのビルド

ドライバーの作成者は、基本クラス、およびその他のすべてを格納するのに 1 つのマスター MOF テキスト ファイルを使用できます。

使用することができます、 [MOF コンパイラ](compiling-a-driver-s-mof-file.md)言語に依存しないクラスと特定の言語の修正されたクラスを格納するファイルを格納しているファイルを生成します。

```cpp
mofcomp -amendment:namespace [ -MOF:mof] [ -MFL:mfl] masterfile
```

*名前空間*パラメーターの形式は、MS\_*XXX*ここで、 *XXX*を生成する、ロケールの LCID です。 作成された mof ファイルには、言語に依存しないクラスが含まれています、mfl ファイル作成には、修正したクラスが含まれています。

NT ベースのオペレーティング システムでは、ドライバーをビルドする場合は、コピー コマンドを使用して 2 つのファイルをマージできます。 Windows 98/私は、[コピー] コマンドは正しく付けず Unicode ファイルに、次のコマンドを使用できます。

```cpp
wmimofck localizedfile -ymof -zmfl
```

1 つのテキスト ファイルには、任意の数の言語を組み合わせることができます。

ローカライズされたファイルは、ローカライズされていないいる MOF ファイルと同じ方法でのバイナリ ファイルにコンパイルできます。

```cpp
mofcomp -B:binaryfile localizedfile
```

単一言語バージョンの Windows には、ドライバーはバイナリの MOF リソースとしてドライバー イメージをアタッチします。 参照してください[ドライバーの MOF ファイルをコンパイルする](compiling-a-driver-s-mof-file.md)詳細についてはします。

MUI のシステム上には、米国英語にドライバー イメージ自体を構築する必要があります。 各インストールは、各追加言語の適切な %windir% で別のイメージ ファイルにリソースとしてバイナリの MOF ファイルをローカライズされた\\system32\\ドライバー\\MUI\\*langid*ディレクトリで*langid*ロケール (たとえば、米国英語の 409) の 16 進数の LCID です。 ファイル名は、いずれかを指定する必要があります*drivername.sys*または*drivername.sys*.mui、場所*drivername.sys*がドライバーの名前をバイナリ。

### <a name="building-one-mof-file-for-all-supported-languages"></a>サポートされているすべての言語の 1 つの MOF ファイルの構築

サポートされている言語ごと、ドライバーのイメージに含まれる場合は、単純なすべての言語をサポートしている MOF ファイルを構築する方法です。 使用して**\#プラグマ**ディレクティブで MOF のテキスト ファイル ドライバーがすべて修正したクラスは、1 つのバイナリの結合もできます。 各ローカライズは、別個の名前空間に存在しているために、1 つのバイナリに、安全に組み合わせることできます。

ドライバー作成者が各修正したクラスの宣言を付ける必要があります、結合された MOF テキスト ファイルを書き込むときに、 **\#プラグマ**ようディレクティブ

```cpp
#pragma namespace ("namespace")
```

場所`namespace`宣言の正しい名前空間です。 たとえば、米国英語の修正されたクラス宣言の前に形式の宣言する必要があります。

```cpp
#pragma namespace ("\\\\.\\root\\wmi\\ms_409")
```

たとえばを宣言するクラスとその修正としては、次のようにします。

```cpp
#pragma namespace ("\\\\.\\root\\wmi)

[guid(xxxxxxxx-xxxx-xxxx-xxxxxxxxxxxx)]
class MyClass 
{
}

#pragma namespace(\\\\.\\root\\wmi\\ms_409)
[amendment, locale(0x407)]
class MyClass
{
}
```

このアプローチを使用して、バイナリの MOF ファイルを構築は、ローカライズされていない方法と同じです。 参照してください[ドライバーの MOF ファイルをコンパイルする](compiling-a-driver-s-mof-file.md)詳細についてはします。

 

 




